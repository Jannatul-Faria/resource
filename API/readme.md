# API কীভাবে তৈরি করবেন এবং এটি PHP-তে কীভাবে কাজ করে?

একটি **API (Application Programming Interface)** হলো বিভিন্ন অ্যাপ্লিকেশন বা সার্ভারের মধ্যে ডেটা আদান-প্রদানের জন্য একটি ইন্টারফেস বা মধ্যস্থতাকারী। PHP-তে API সাধারণত **RESTful API** হিসেবে তৈরি করা হয়, যেখানে ক্লায়েন্ট (যেমন ফ্রন্টএন্ড অ্যাপ্লিকেশন বা মোবাইল অ্যাপ) HTTP প্রোটোকল ব্যবহার করে সার্ভারের সাথে ডেটা আদান-প্রদান করে।

RESTful API-এর মাধ্যমে আমরা HTTP মেথডগুলো (GET, POST, PUT, DELETE) ব্যবহার করে বিভিন্ন অ্যাকশন পরিচালনা করতে পারি। PHP ব্যবহার করে একটি RESTful API তৈরি করা খুব সহজ।

### PHP তে API তৈরি করার ধাপ:

#### ১. API রাউটিং তৈরি করা
প্রথমে, আমরা কিছু নির্দিষ্ট URL বা রুট তৈরি করব, যা বিভিন্ন HTTP মেথড হ্যান্ডেল করবে।

#### ২. HTTP মেথড হ্যান্ডলিং (GET, POST, PUT, DELETE)
প্রতিটি মেথডের জন্য আমরা আলাদা আলাদা ফাংশন তৈরি করব যা নির্দিষ্ট অপারেশন সম্পাদন করবে, যেমন ডেটা রিড করা, যোগ করা, আপডেট করা বা মুছে ফেলা।

#### ৩. ডেটা ফরম্যাট (JSON)
API সাধারণত JSON ফরম্যাটে ডেটা পাঠায় এবং গ্রহণ করে, তাই আমাদের ডেটাকে JSON আকারে এনকোড করতে হবে এবং ক্লায়েন্টে পাঠাতে হবে।

### উদাহরণ: একটি সহজ PHP API

ধরা যাক আমরা একটি **To-Do লিস্ট API** তৈরি করছি, যেখানে আমরা টাস্কগুলো যুক্ত করা, দেখা, আপডেট করা, এবং মুছে ফেলার কাজ করব।

#### ১. ডাটাবেজ কানেকশন (MySQL):
```php
<?php
$host = "localhost";
$db_name = "api_db";
$username = "root";
$password = "";

try {
    $conn = new PDO("mysql:host=$host;dbname=$db_name", $username, $password);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
?>
```

#### ২. API রাউটিং এবং HTTP মেথড হ্যান্ডলিং:
```php
<?php
header("Content-Type: application/json");

// রাউট চেক করা
$requestMethod = $_SERVER["REQUEST_METHOD"];

// বিভিন্ন HTTP মেথড হ্যান্ডল করা
switch ($requestMethod) {
    case 'GET':
        getTasks();
        break;
    case 'POST':
        addTask();
        break;
    case 'PUT':
        updateTask();
        break;
    case 'DELETE':
        deleteTask();
        break;
    default:
        echo json_encode(["message" => "Invalid Request"]);
        break;
}

// GET মেথড: সমস্ত টাস্ক রিটার্ন করা
function getTasks() {
    global $conn;
    $query = "SELECT * FROM tasks";
    $stmt = $conn->prepare($query);
    $stmt->execute();
    $tasks = $stmt->fetchAll(PDO::FETCH_ASSOC);
    echo json_encode($tasks);
}

// POST মেথড: নতুন টাস্ক যোগ করা
function addTask() {
    global $conn;
    $data = json_decode(file_get_contents("php://input"), true);
    $query = "INSERT INTO tasks (title, description) VALUES (:title, :description)";
    $stmt = $conn->prepare($query);
    $stmt->bindParam(":title", $data['title']);
    $stmt->bindParam(":description", $data['description']);
    if ($stmt->execute()) {
        echo json_encode(["message" => "Task added successfully"]);
    } else {
        echo json_encode(["message" => "Failed to add task"]);
    }
}

// PUT মেথড: টাস্ক আপডেট করা
function updateTask() {
    global $conn;
    $data = json_decode(file_get_contents("php://input"), true);
    $query = "UPDATE tasks SET title = :title, description = :description WHERE id = :id";
    $stmt = $conn->prepare($query);
    $stmt->bindParam(":title", $data['title']);
    $stmt->bindParam(":description", $data['description']);
    $stmt->bindParam(":id", $data['id']);
    if ($stmt->execute()) {
        echo json_encode(["message" => "Task updated successfully"]);
    } else {
        echo json_encode(["message" => "Failed to update task"]);
    }
}

// DELETE মেথড: টাস্ক মুছে ফেলা
function deleteTask() {
    global $conn;
    $data = json_decode(file_get_contents("php://input"), true);
    $query = "DELETE FROM tasks WHERE id = :id";
    $stmt = $conn->prepare($query);
    $stmt->bindParam(":id", $data['id']);
    if ($stmt->execute()) {
        echo json_encode(["message" => "Task deleted successfully"]);
    } else {
        echo json_encode(["message" => "Failed to delete task"]);
    }
}
?>
```

#### ৩. ডেটাবেস টেবিল তৈরি করা:
```sql
CREATE TABLE tasks (
    id INT(11) AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description TEXT NOT NULL
);
```

### কীভাবে API কাজ করে:
1. **GET মেথড**: যখন ক্লায়েন্ট একটি GET রিকোয়েস্ট পাঠাবে `/api/tasks` এ, তখন সমস্ত টাস্কের ডেটা JSON ফরম্যাটে পাঠানো হবে।
2. **POST মেথড**: নতুন টাস্ক যোগ করার জন্য `/api/tasks`-এ POST রিকোয়েস্ট পাঠানো হবে, সাথে টাস্কের `title` এবং `description` ডেটা।
3. **PUT মেথড**: টাস্ক আপডেট করতে, PUT রিকোয়েস্ট পাঠিয়ে টাস্কের `id`, `title`, এবং `description` প্রদান করতে হবে।
4. **DELETE মেথড**: একটি টাস্ক মুছে ফেলার জন্য DELETE রিকোয়েস্ট পাঠাতে হবে এবং টাস্কের `id` প্রদান করতে হবে।

### JSON ফরম্যাটে রেসপন্স
প্রতিটি রিকোয়েস্টে API JSON ফরম্যাটে রেসপন্স প্রদান করে, যা সাধারণত ফ্রন্টএন্ড অ্যাপ্লিকেশন (যেমন React বা Angular) সহজে হ্যান্ডেল করতে পারে।

### সারসংক্ষেপ:
- PHP-তে API তৈরি করার সময়, আপনি HTTP মেথডের (GET, POST, PUT, DELETE) মাধ্যমে ডেটা পরিচালনা করেন।
- ডেটাবেজের সাথে ইন্টারঅ্যাক্ট করে এবং JSON ফরম্যাটে রেসপন্স দেয়।
- API-এর মাধ্যমে আপনি ডাইনামিক ওয়েবসাইট বা মোবাইল অ্যাপ্লিকেশনের সাথে সার্ভার কমিউনিকেশন সহজে করতে পারেন।

API তৈরি করার জন্য PHP একটি খুবই সহজ এবং কার্যকর প্ল্যাটফর্ম।