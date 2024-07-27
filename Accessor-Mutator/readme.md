# <b> Accessor & Mutator </b>
Laravel এ, অ্যাক্সেসর (Accessor) এবং মিউটেটর (Mutator) হল এমন ফাংশন যা মডেলের অ্যাট্রিবিউটগুলিকে পড়া ও লেখা করার সময় চালিত হয়। এগুলি ব্যবহার করে আপনি মডেলের অ্যাট্রিবিউটগুলিকে প্রাপ্তি ও সংরক্ষণের আগে রূপান্তর করতে পারেন।

### অ্যাক্সেসর (Accessor)

অ্যাক্সেসর ব্যবহার করে আপনি যখন মডেলের কোন অ্যাট্রিবিউট পড়বেন তখন তা কিভাবে রূপান্তর হবে তা নির্ধারণ করতে পারেন। উদাহরণস্বরূপ, যদি আপনি চান যে নামের প্রথম অক্ষর সর্বদা বড় হরফে থাকুক, তাহলে আপনি একটি অ্যাক্সেসর ব্যবহার করতে পারেন।

```php
<?php

namespace App\\Models;

use Illuminate\\Database\\Eloquent\\Model;

class User extends Model
{
    // অ্যাক্সেসর
    public function getNameAttribute($value)
    {
        return ucfirst($value);
    }
}

```

### মিউটেটর (Mutator)

মিউটেটর ব্যবহার করে আপনি যখন মডেলের কোন অ্যাট্রিবিউট লিখবেন তখন তা কিভাবে রূপান্তর হবে তা নির্ধারণ করতে পারেন। উদাহরণস্বরূপ, যদি আপনি চান যে নাম সর্বদা ছোট হরফে সংরক্ষিত হোক, তাহলে আপনি একটি মিউটেটর ব্যবহার করতে পারেন।

```php
<?php

namespace App\\Models;

use Illuminate\\Database\\Eloquent\\Model;

class User extends Model
{
    // মিউটেটর
    public function setNameAttribute($value)
    {
        $this->attributes['name'] = strtolower($value);
    }
}

```

এইভাবে, অ্যাক্সেসর এবং মিউটেটর ব্যবহার করে আপনি সহজেই আপনার মডেলের অ্যাট্রিবিউটগুলির মান নিয়ন্ত্রণ করতে পারেন।