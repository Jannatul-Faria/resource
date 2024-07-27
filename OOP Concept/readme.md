# OOP Concept

[**১. অবজেক্ট ওরিয়েন্টেড পিএইচপি: Classes & Objects**]()

[**২. অবজেক্ট ওরিয়েন্টেড পিএইচপি: $this Keyword**]()

[**৩. অবজেক্ট ওরিয়েন্টেড পিএইচপি: Access Modifiers**]()

[**৪. অবজেক্ট ওরিয়েন্টেড পিএইচপি: Inheritance**]()

অবজেক্ট-ওরিয়েন্টেড প্রোগ্রামিং (OOP) হল প্রোগ্রামিং প্যারাডাইম যা অবজেক্ট ভিত্তিক। OOP-তে চারটি প্রধান পিলার বা স্তম্ভ আছে: এনক্যাপসুলেশন, ইনহেরিটেন্স, পলিমরফিজম, এবং অ্যাবস্ট্রাকশন। নিচে বাংলায় এই পিলারগুলো সংক্ষেপে আলোচনা করা হল:

### ১. এনক্যাপসুলেশন (Encapsulation)

এনক্যাপসুলেশন হল ডেটা এবং মেথডগুলোকে একসাথে একটি ইউনিট হিসেবে গুছিয়ে রাখা। এতে ডেটা বাইরে থেকে সরাসরি পরিবর্তন করা যায় না, বরং নির্দিষ্ট মেথডের মাধ্যমে এক্সেস করতে হয়। এটি ডেটার সিকিউরিটি নিশ্চিত করে।

### ২. ইনহেরিটেন্স (Inheritance)

ইনহেরিটেন্স হল এক ক্লাসের প্রোপার্টি ও মেথডগুলো আরেক ক্লাসে ব্যবহার করার পদ্ধতি। এটি কোডের পুনরায় ব্যবহারযোগ্যতা বৃদ্ধি করে এবং সম্পর্কিত ক্লাসগুলোকে একটি নির্দিষ্ট ধারায় সাজাতে সাহায্য করে।

### ৩. পলিমরফিজম (Polymorphism)

পলিমরফিজম হল একই মেথড বিভিন্ন কনটেক্সটে ভিন্নভাবে ব্যবহার করা। এটি মূলত মেথড ওভাররাইডিং এবং ওভারলোডিং-এর মাধ্যমে অর্জিত হয়।

### ৪. অ্যাবস্ট্রাকশন (Abstraction)

অ্যাবস্ট্রাকশন হল শুধুমাত্র প্রয়োজনীয় ডিটেইলগুলো প্রকাশ করা এবং বাকি ডিটেইলগুলো লুকিয়ে রাখা। এটি সাধারণত অ্যাবস্ট্রাক্ট ক্লাস এবং ইন্টারফেসের মাধ্যমে অর্জিত হয়।

এই চারটি পিলার OOP-এর মূল ধারণা এবং প্রোগ্রামিং প্র্যাকটিসের মেরুদণ্ড হিসেবে কাজ করে। আশা করি এই উত্তরগুলো আপনার ইন্টারভিউ প্রস্তুতিতে সাহায্য করবে।

**1.এনক্যাপসুলেশন (Encapsulation)**

```php
<?php
class Person {
    private $name;  // Private প্রপার্টি

    // Setter method
    public function setName($name) {
        $this->name = $name;
    }

    // Getter method
    public function getName() {
        return $this->name;
    }
}
?>

```

**2.ইনহেরিটেন্স (Inheritance)**

```php
<?php
class Animal {
    public $name;

    public function makeSound() {
        echo "Some sound";
    }
}

class Dog extends Animal {
    public function makeSound() {
        echo "Bark";
    }
}

$dog = new Dog();
$dog->makeSound();  // Output: Bark
?>

```

**3.পলিমরফিজম (Polymorphism)**

```php
<?php
class Shape {
    public function draw() {
        echo "Drawing a shape";
    }
}

class Circle extends Shape {
    public function draw() {
        echo "Drawing a circle";
    }
}

class Square extends Shape {
    public function draw() {
        echo "Drawing a square";
    }
}

$shapes = [new Circle(), new Square()];

foreach ($shapes as $shape) {
    $shape->draw();
}
// Output:
// Drawing a circle
// Drawing a square
?>

```

**4. অ্যাবস্ট্রাকশন (Abstraction)**

```php
<?php
abstract class Vehicle {
    abstract public function startEngine();

    public function displayType() {
        echo "This is a vehicle";
    
}

class Car extends Vehicle {
    public function startEngine() {
        echo "Starting car engine";
    }
}

$car = new Car();
$car->startEngine();  // Output: Starting car engine
$car->displayType();  // Output: This is a vehicle
?>

```