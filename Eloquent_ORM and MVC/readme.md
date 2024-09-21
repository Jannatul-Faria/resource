# **Eloquent ORM** এবং **MVC প্যাটার্ন** PHP Laravel এ কীভাবে কাজ করে :

### Eloquent ORM:
Eloquent ORM (Object-Relational Mapping) হলো Laravel এর ডাটাবেজ ব্যবস্থাপনার জন্য ব্যবহৃত একটি শক্তিশালী টুল। এটি মডেল (Model) এর মাধ্যমে ডাটাবেজ টেবিলের সাথে সম্পর্ক স্থাপন করে এবং ডাটাবেজ অপারেশনগুলোকে খুব সহজ এবং কার্যকরী করে তোলে। Eloquent ORM এর মাধ্যমে Laravel এ ডাটাবেজ টেবিলগুলোর সাথে মডেল এর মাধ্যমে কাজ করা হয়, যাতে কোড সহজে পড়া এবং বজায় রাখা যায়। 

Eloquent এর সুবিধা হলো, ডাটাবেজ কুয়েরি করার জন্য SQL জানার দরকার হয় না; মডেল ব্যবহার করেই কুয়েরি করা যায়। উদাহরণস্বরূপ, নিচের কোডটি Eloquent ব্যবহার করে একটি টেবিল থেকে সকল ডাটার তথ্য নিয়ে আসছে:
```php
$users = User::all();
```
এখানে `User` হলো মডেল, এবং `all()` মেথডটি দিয়ে সকল ডাটা আনা হচ্ছে।

### MVC (Model-View-Controller):
MVC হলো একটি সফটওয়্যার ডিজাইন প্যাটার্ন যা Laravel ফ্রেমওয়ার্কে ব্যবহৃত হয়। এটি অ্যাপ্লিকেশনের লজিক এবং উপস্থাপনাকে আলাদা করে কাজ করে। MVC এর তিনটি প্রধান অংশ হলো:

1. **Model**: ডাটাবেজের সাথে সরাসরি যোগাযোগ করে এবং ডাটাবেজ থেকে ডাটা নিয়ে আসে, অথবা ডাটাবেজে ডাটা সেভ করে। Eloquent ORM মডেল হিসেবে ব্যবহৃত হয়।
   
2. **View**: এটি অ্যাপ্লিকেশনের UI বা ফ্রন্টএন্ড অংশকে নির্দেশ করে, যা ব্যবহারকারী দেখতে পায়। Laravel এ Blade টেমপ্লেট ইঞ্জিন ব্যবহৃত হয় View তৈরি করার জন্য।
   
3. **Controller**: এটি Model এবং View এর মধ্যে সমন্বয়কারী হিসেবে কাজ করে। Controller ব্যবহারকারী থেকে ইনপুট নিয়ে সেই অনুযায়ী Model থেকে ডাটা এনে View তে উপস্থাপন করে। 

উদাহরণস্বরূপ, একজন ব্যবহারকারী যদি কোনো প্রোডাক্টের তালিকা দেখতে চায়, তাহলে Controller মডেল থেকে ডাটা নিয়ে View তে পাঠায়, এবং View সেই ডাটা ব্যবহারকারীর ব্রাউজারে দেখায়।

**Laravel এ কাজ করার পদ্ধতি:**
Laravel এ কাজ করতে গেলে প্রথমে আপনাকে একটি মডেল তৈরি করতে হবে, যাতে ডাটাবেজের টেবিলের সাথে সম্পর্ক থাকে। এরপর সেই মডেল এর ডাটা নিয়ন্ত্রণ করতে একটি Controller তৈরি করতে হবে, এবং সেই ডাটা প্রদর্শনের জন্য একটি View তৈরি করা হবে।