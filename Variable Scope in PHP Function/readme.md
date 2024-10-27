# Variable Scope in PHP Function
PHP তে **Variable Scope** বলতে একটি ভেরিয়েবল কোথা থেকে অ্যাক্সেস বা ব্যবহার করা যাবে সেটি বোঝানো হয়। PHP তে সাধারণত তিন ধরনের ভেরিয়েবল স্কোপ আছে:

1. **Global Scope**
2. **Local Scope**
3. **Static Scope**

প্রতিটি স্কোপ সম্পর্কে নিচে বিস্তারিত আলোচনা করা হলো।

---

### 1. Global Scope
একটি ভেরিয়েবল যখন কোন ফাংশনের বাইরের স্থানে ডিক্লেয়ার করা হয়, তখন সেটি গ্লোবাল স্কোপের মধ্যে থাকে। গ্লোবাল ভেরিয়েবল ফাংশনের বাইরে থেকে সরাসরি অ্যাক্সেসযোগ্য হলেও, ফাংশনের ভেতর থেকে সরাসরি ব্যবহার করা যায় না। ফাংশনের ভেতর থেকে অ্যাক্সেস করতে হলে `global` কীওয়ার্ড ব্যবহার করতে হয়, অথবা `$GLOBALS` অ্যারের মাধ্যমে ভেরিয়েবলকে ফাংশনে আনতে হয়।

**উদাহরণ:**

```php
<?php
$globalVar = "আমি গ্লোবাল ভেরিয়েবল"; // গ্লোবাল স্কোপে ডিক্লেয়ার

function testGlobal() {
    global $globalVar; // গ্লোবাল ভেরিয়েবল অ্যাক্সেস করতে
    echo $globalVar;
}

testGlobal(); // আউটপুট: আমি গ্লোবাল ভেরিয়েবল
?>
```

এখানে `$globalVar` ভেরিয়েবলটি গ্লোবাল স্কোপে আছে এবং `global` কীওয়ার্ড ব্যবহার করে ফাংশনের ভেতর থেকে এটি অ্যাক্সেস করা হয়েছে।

---

### 2. Local Scope
একটি ভেরিয়েবল যখন কোন ফাংশনের ভিতরে ডিক্লেয়ার করা হয়, তখন সেটি শুধুমাত্র সেই ফাংশনের ভেতরেই অ্যাক্সেসযোগ্য থাকে। এই ধরনের ভেরিয়েবলকে **Local Variable** বলা হয় এবং এটি ফাংশনের বাইরে থেকে সরাসরি অ্যাক্সেস করা যায় না।

**উদাহরণ:**

```php
<?php
function testLocal() {
    $localVar = "আমি লোকাল ভেরিয়েবল"; // লোকাল স্কোপে ডিক্লেয়ার
    echo $localVar;
}

testLocal(); // আউটপুট: আমি লোকাল ভেরিয়েবল
// echo $localVar; // এই লাইনটি ত্রুটি দিবে কারণ $localVar ফাংশনের বাইরে অ্যাক্সেসযোগ্য নয়।
?>
```

এখানে `$localVar` শুধুমাত্র `testLocal` ফাংশনের মধ্যে ব্যবহারযোগ্য এবং ফাংশনের বাইরে এটি অ্যাক্সেস করা সম্ভব নয়।

---

### 3. Static Scope
Static স্কোপ ব্যবহার করা হয় কোন ভেরিয়েবলকে ফাংশনের মধ্যে ডিক্লেয়ার করে ফাংশন কলের মধ্যবর্তী মান সংরক্ষণ করার জন্য। প্রতিবার ফাংশন কল করলে ভেরিয়েবলের মান পুনরায় ইনিশিয়ালাইজ না করে পূর্বের মান সংরক্ষণ করা হয়। `static` কীওয়ার্ড ব্যবহার করে স্ট্যাটিক স্কোপ ডিক্লেয়ার করা হয়।

**উদাহরণ:**

```php
<?php
function testStatic() {
    static $count = 0; // স্ট্যাটিক ভেরিয়েবল
    $count++;
    echo $count . "<br>";
}

testStatic(); // আউটপুট: 1
testStatic(); // আউটপুট: 2
testStatic(); // আউটপুট: 3
?>
```

এখানে `$count` ভেরিয়েবলটি স্ট্যাটিক ভাবে ডিক্লেয়ার করা হয়েছে, ফলে প্রতিবার `testStatic` ফাংশন কলের সময় `$count` এর পূর্বের মান সংরক্ষিত থাকে এবং ১ করে বৃদ্ধি পায়।

---

### সারসংক্ষেপ
PHP তে স্কোপ নির্ধারণ করে দেয় কোন ভেরিয়েবল কোথায় ব্যবহারযোগ্য এবং কোন অংশ থেকে তা অ্যাক্সেস করা যাবে। এই স্কোপগুলো সঠিকভাবে ব্যবহারের মাধ্যমে কোডের কার্যক্ষমতা এবং নিরাপত্তা নিশ্চিত করা যায়।