# MN Online Shopping: লাইভ করার স্টার্টার

এই প্রজেক্টটি Vercel-এ `mn-online-shopping.vercel.app`-এর মতো ফ্রি সাবডোমেইনে প্রকাশের জন্য তৈরি। **এখনো লাইভ/ডেপ্লয় করা হয়নি।** ডেপ্লয় করতে আপনার নিজের Vercel ও Supabase অ্যাকাউন্টে লগইন করে নিচের ধাপগুলো করতে হবে।

## ১) Supabase ডেটাবেজ ও ছবি স্টোরেজ
1. https://supabase.com এ ফ্রি অ্যাকাউন্ট খুলে New project তৈরি করুন।
2. Project-এর **SQL Editor** খুলুন।
3. এই ZIP-এর `supabase/setup.sql` ফাইলের সব SQL কপি করে Run করুন।
4. Authentication → Users থেকে আপনার অ্যাডমিন ইমেইল দিয়ে একটি user তৈরি করুন। নিরাপদ পাসওয়ার্ড দিন।
5. Project Settings → API থেকে Project URL এবং `anon` public key কপি করুন। `service_role` key কখনো ওয়েবসাইটে দেবেন না।

## ২) Vercel-এ প্রকাশ
1. https://vercel.com এ অ্যাকাউন্ট খুলুন।
2. এই ZIP-টি কম্পিউটারে Extract করে GitHub-এ নতুন repository-তে আপলোড করুন।
3. Vercel → Add New → Project থেকে repository Import করুন।
4. Environment Variables-এ এই দুইটি variable যোগ করুন:
   - `NEXT_PUBLIC_SUPABASE_URL` = Supabase Project URL
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY` = Supabase anon public key
5. Deploy চাপুন। Vercel একটি `*.vercel.app` ঠিকানা দেবে। চাইলে Project Settings → Domains-এ গিয়ে `mn-online-shopping.vercel.app` নামটি availability অনুযায়ী সেট করুন।

## ৩) চালানো/পরীক্ষা
লোকাল কম্পিউটারে Node.js ইনস্টল করে:
```bash
npm install
cp .env.example .env.local
# .env.local-এ Supabase URL ও anon key বসান
npm run dev
```
তারপর http://localhost:3000 খুলুন।

## সাইটে যা আছে
- পণ্য ক্যাটাগরি, সার্চ, কার্ট ও অর্ডার ফর্ম
- COD, bKash Manual, Nagad Manual payment option
- Supabase-এ পণ্য, অর্ডার ও ছবি সংরক্ষণ
- Supabase Auth দিয়ে অ্যাডমিন লগইন
- অ্যাডমিন থেকে পণ্য যোগ/মুছুন, অর্ডার দেখুন ও স্ট্যাটাস বদলান

## গুরুত্বপূর্ণ নিরাপত্তা ও পেমেন্ট নোট
- এই SQL নীতিমালা ধরে নেয় Supabase Auth-এর যেকোনো authenticated account-কে অ্যাডমিন ধরা হবে। **অ্যাডমিন user শুধু আপনি তৈরি করবেন, কাউকে sign-up সুবিধা দেবেন না।** পরে চাইলে আলাদা admin-role policy করা উচিত।
- bKash/Nagad এখানে শুধু Manual পদ্ধতি নির্বাচন। স্বয়ংক্রিয় টাকা গ্রহণের জন্য অনুমোদিত merchant account, gateway credentials ও server-side integration লাগবে।
- ফ্রি প্ল্যানে স্টোরেজ/ট্রাফিক/ব্যবহারের সীমা থাকে। “সম্পূর্ণ বিনামূল্যে, সীমাহীন” নিশ্চয়তা কোনো ফ্রি হোস্টিংয়ে দেওয়া যায় না।
- লাইভে যাওয়ার আগে একটি পরীক্ষামূলক অর্ডার দিয়ে সব যাচাই করুন।
