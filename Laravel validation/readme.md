Validation হল একটি প্রক্রিয়া যার মাধ্যমে ইউজার থেকে প্রাপ্ত ইনপুট ডেটার সঠিকতা এবং মান পরীক্ষা করা হয়। এটি নিশ্চিত করে যে ইউজার যে ডেটা প্রদান করছে, তা সঠিক এবং পূর্বনির্ধারিত শর্তের সাথে মিলছে। Laravel-এর মতো ফ্রেমওয়ার্কে, Validation সাধারণত ব্যবহারকারীর ফর্ম সাবমিশনের সময় করা হয়, যেমন: নাম, ইমেইল, ফোন নম্বর, পাসওয়ার্ড ইত্যাদি। 

Laravel এ Validation:
Laravel এ Validation খুবই সহজ এবং শক্তিশালী। আপনি যেকোনো ফর্ম ডেটা বা ইনপুট ভ্যালিডেট করতে পারেন একাধিক validation rules ব্যবহার করে।

## Laravel এর Validation কিভাবে কাজ করে?

Laravel এ Validation সাধারণত দুটি পদ্ধতিতে করা যায়:

1. Controller Validation: 
    - Form Request Validation: যখন আপনি কোন ফর্মের জন্য কাস্টম ভ্যালিডেশন তৈরি করতে চান, তখন Form Request ক্লাস ব্যবহার করা হয়।
    - Inline Validation: কোডে সরাসরি ভ্যালিডেশন চেক করা হয়।

১. Controller Validation:

Laravel এ controller method এ *validate()* মেথড ব্যবহার করে সরাসরি ইনপুট ভ্যালিডেশন করা যায়।

উদাহরণ:
```php
public function store(Request request){
    // ফর্ম ইনপুট ভ্যালিডেশন
    validated = $request->validate([
        'name' => 'required|string|max:255', // নাম অবশ্যই পূর্ণাঙ্গ হতে হবে
        'email' => 'required|email|unique:users,email', // ইমেইল ফরম্যাট সঠিক এবং ইউনিক হতে হবে
        'password' => 'required|string|min:8|confirmed', // পাসওয়ার্ড কমপক্ষে ৮ অক্ষরের হতে হবে
    ]);
    
    // ইনপুট ভ্যালিডেশন সফল হলে, ডাটা সেভ করা যাবে
    User::create([
        'name' =>request->name,
        'email' => request->email,
        'password' => bcrypt(request->password),
    ]);

    return redirect()->route('users.index');
}
```

২. *Form Request Validation:*

এটি একটি বিশেষ ক্লাস যা ভ্যালিডেশন লজিক আলাদা করে রাখতে সাহায্য করে। এই পদ্ধতিতে, আপনি একটি আলাদা ক্লাস তৈরি করেন যেটি ডেটা ভ্যালিডেশনের কাজ করে।

*উদাহরণ:*
1. প্রথমে *Form Request* ক্লাস তৈরি করতে হবে:
```
php artisan make:request StoreUserRequest
```

2. তৈরি হওয়া *StoreUserRequest* ক্লাসে ভ্যালিডেশন রুলস যুক্ত করুন:
```php
namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class StoreUserRequest extends FormRequest
{
    public function authorize()
    {
        return true;  // শুধু যদি আপনি চাইলে এখানে অনুমতি চেক করতে পারেন
    }

    public function rules()
    {
        return [
            'name' => 'required|string|max:255',
            'email' => 'required|email|unique:users,email',
            'password' => 'required|string|min:8|confirmed',
        ];
    }
}
```

3. তারপর *Controller* এ এই *Request* ক্লাস ব্যবহার করুন:
```php
use App\Http\Requests\StoreUserRequest;

public function store(StoreUserRequest request){

    // ফর্ম ইনপুট ভ্যালিডেশন সফল হলে, ডাটা সেভ করা যাবে
    User::create([
        'name' =>request->name,
        'email' => request->email,
        'password' => bcrypt(request->password),
    ]);

    return redirect()->route('users.index');
}
```

Laravel Validation Rules:
Laravel এ অনেক ধরনের validation rules রয়েছে যা দিয়ে আপনি ইউজারের ইনপুট যাচাই করতে পারেন। নিচে কিছু সাধারণ validation rules এর তালিকা দেওয়া হলো:

- required: ইনপুট ফিল্ডটি খালি থাকতে পারবে না।
- email: ইনপুট ফিল্ডটি সঠিক ইমেইল ফরম্যাটে থাকতে হবে।
- max:<value>: ইনপুটটির সর্বোচ্চ দৈর্ঘ্য কত হতে হবে।
- min:<value>: ইনপুটটির সর্বনিম্ন দৈর্ঘ্য কত হতে হবে।
- unique:<table,column>: ইনপুট ফিল্ডটির মান ডাটাবেসে ইউনিক হতে হবে। যেমন: 'email' => 'unique:users,email'।
- confirmed: পাসওয়ার্ড বা অন্য যেকোনো ফিল্ডের জন্য দুটি ইনপুট (যেমন "password" এবং "password_confirmation") ম্যাচ করতে হবে।
- numeric: ইনপুটটি শুধুমাত্র সংখ্যা হতে হবে।
- string: ইনপুটটি একটি স্ট্রিং হতে হবে।
- alpha: ইনপুটটি শুধুমাত্র অক্ষর (alphabet) হতে হবে।
- boolean: ইনপুটটি true বা false হতে হবে।
- date: ইনপুটটি একটি বৈধ তারিখ হতে হবে।

Error Messages:
যদি ইনপুট ভ্যালিডেশন ব্যর্থ হয়, তবে Laravel নিজেই ডিফল্ট error messages প্রদান করে। আপনি যদি কাস্টম error messages দিতে চান, তবে তা language files অথবা মেসেজ এর মাধ্যমে কাস্টমাইজ করতে পারেন।

উদাহরণ:
```php
validated =request->validate([
    'name' => 'required|string|max:255',
    'email' => 'required|email|unique:users,email',
    'password' => 'required|string|min:8|confirmed',
], [
    'name.required' => 'নামটি পূর্ণ করতে হবে!',
    'email.required' => 'ইমেইলটি প্রদান করতে হবে!',
    'password.min' => 'পাসওয়ার্ড কমপক্ষে ৮ অক্ষরের হতে হবে!',
]);
```

Laravel Validation এর সুবিধা:
1. সহজ ও কার্যকর: Laravel এর ভ্যালিডেশন খুবই সহজ এবং সরল। কোড কমপ্লেক্সিটি অনেক কমে যায়।
2. কাস্টম মেসেজ: আপনি চাইলে কাস্টম মেসেজ যোগ করতে পারেন।
3. ইউটিলিটি: বিভিন্ন ধরনের ভ্যালিডেশন রুলস যেমন required, email, unique ইত্যাদি ব্যবহার করা যায়।
4. Form Request ব্যবহারের মাধ্যমে কন্ট্রোলারকে পরিষ্কার রাখা যায়।

#### সারাংশ:
Laravel এ Validation ব্যবহার করা হলে আপনি সহজেই ইউজারের ইনপুট যাচাই করতে পারবেন এবং নিশ্চিত করতে পারবেন যে ইনপুট ডেটা সঠিক, সুরক্ষিত এবং পূর্বনির্ধারিত শর্ত পূরণ করছে। এটি সঠিক তথ্য সংগ্রহ এবং নিরাপদ ডেটাবেস ব্যবহারের জন্য অত্যন্ত গুরুত্বপূর্ণ।

