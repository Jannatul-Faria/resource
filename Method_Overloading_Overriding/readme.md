# মেথড ওভারলোডিং (Method Overloading)/মেথড ওভাররাইটিং (Method Overriding):

PHP-তে **মেথড ওভারলোডিং (Method Overloading)** এবং **মেথড ওভাররাইটিং (Method Overriding)** হলো দুটি ভিন্ন ধারণা। এগুলো অবজেক্ট ওরিয়েন্টেড প্রোগ্রামিং (OOP) এর গুরুত্বপূর্ণ বৈশিষ্ট্য। এবার আমরা এগুলোকে ব্যাখ্যা করব:

### মেথড ওভারলোডিং (Method Overloading):
মেথড ওভারলোডিং বলতে বোঝায় একই নামের একাধিক মেথড তৈরি করা, কিন্তু তাদের প্যারামিটার ভিন্ন থাকে। অনেক প্রোগ্রামিং ভাষায় (যেমন: জাভা) এটি সমর্থন করে, কিন্তু PHP-তে সরাসরি মেথড ওভারলোডিং নেই। অর্থাৎ, PHP তে আপনি একই নামের মেথড আলাদা আলাদা প্যারামিটারের সাথে ডিফাইন করতে পারবেন না। তবে __call() ম্যাজিক মেথড ব্যবহার করে কিছুটা ওভারলোডিংয়ের মতো আচরণ করতে পারেন।

**PHP তে মেথড ওভারলোডিং এর সীমাবদ্ধতা:**  
PHP তে মেথড ওভারলোডিং সরাসরি সমর্থিত নয়। একই নামের মেথড একাধিকবার ডিফাইন করা যায় না। তবে, ম্যাজিক মেথড `__call()` ব্যবহার করে কিছুটা ওভারলোডিংয়ের মতো প্রভাব তৈরি করা যায়। উদাহরণস্বরূপ:

```php
class MyClass {
    public function __call($name, $arguments) {
        if ($name == 'add') {
            if (count($arguments) == 2) {
                return $arguments[0] + $arguments[1];
            } elseif (count($arguments) == 3) {
                return $arguments[0] + $arguments[1] + $arguments[2];
            }
        }
    }
}

$obj = new MyClass();
echo $obj->add(2, 3);   // 5
echo $obj->add(2, 3, 4); // 9
```

### মেথড ওভাররাইটিং (Method Overriding):
মেথড ওভাররাইটিং বলতে বোঝায় যখন কোনো subclass (উপশ্রেণী) তার parent class (মূল শ্রেণী) এর একটি মেথডকে পুনঃলিখন (override) করে। এর মাধ্যমে subclass তার নিজের কার্যকারিতা নির্ধারণ করতে পারে। PHP-তে মেথড ওভাররাইটিং সমর্থন করে এবং এটি parent class এর মেথডকে `override` করার মাধ্যমে করা হয়।

**PHP তে মেথড ওভাররাইটিং উদাহরণ:**

```php
class ParentClass {
    public function showMessage() {
        echo "This is the parent class message.";
    }
}

class ChildClass extends ParentClass {
    public function showMessage() {
        echo "This is the child class message.";
    }
}

$obj = new ChildClass();
$obj->showMessage(); // Output: This is the child class message.
```

এখানে, `ChildClass` তার parent `ParentClass` এর `showMessage()` মেথডকে ওভাররাইট করেছে।

**PHP তে মেথড ওভাররাইটিং এর সীমাবদ্ধতা:**
PHP তে মেথড ওভাররাইট করার সময় কিছু নিয়ম মেনে চলতে হয়:
1. <b> Access modifier (public, private, protected)</b> parent এবং child মেথডে একই হতে হবে।
2. Parent মেথডের প্যারামিটারের সংখ্যা ও ধরন child মেথডে থাকা প্রয়োজন।

**সংক্ষেপে:**
- **Method Overloading:** PHP সরাসরি সমর্থন করে না, তবে ম্যাজিক মেথড ব্যবহার করে করা যায়।
- **Method Overriding:** PHP তে সম্পূর্ণভাবে সমর্থিত, যেখানে subclass তার parent class এর মেথডকে পুনঃলিখন করতে পারে।

**মূল পার্থক্য**
- **মেথড ওভারলোডিং:** ম্যাজিক মেথডের মাধ্যমে ডাইনামিক্যালি প্যারামিটারের উপর ভিত্তি করে অজানা মেথডকে হ্যান্ডেল করা হয়।
- **মেথড ওভাররাইডিং:** চাইল্ড ক্লাসে প্যারেন্ট ক্লাসের মেথডকে আবার ডিফাইন করা হয় এবং নতুন ইমপ্লিমেন্টেশন দেওয়া হয়।