# নিটিং ফরমুলা হ্যান্ডবুক

সার্কুলার নিটিং ইন্ডাস্ট্রিতে ব্যবহৃত ৩২টি গুরুত্বপূর্ণ সূত্রের ক্যালকুলেটর — একটাই ফাইলে (`index.html`), কোনো বিল্ড স্টেপ লাগে না।

## কী আছে
সূত্রগুলো ৫টা ক্যাটাগরিতে ভাগ করা:
- **ওজন, GSM ও এরিয়া** — GSM, Fabric Weight, Fabric Area, Yarn Consumption
- **সুতা, কাউন্ট ও কনজাম্পশন** — Stitch Length, Loop Length, Ne/Tex/Denier কনভার্সন, Yarn Required, Reel Length, Yarn Count
- **মেশিন ও নিডেল** — Fabric Width, Tube Diameter, Machine Gauge, Total Needles
- **প্রোডাকশন ও স্পিড** — Production (kg/hr), Machine Efficiency, Take-up Speed, Yarn Delivery Speed, Machine RPM, Fabric Length Produced, Surface Speed
- **ফেব্রিক কোয়ালিটি ও ডেনসিটি** — CPI, WPI, Stitch Density, Cover Factor, Tightness Factor (K), Shrinkage, Spirality

প্রতিটি সূত্রে ট্যাপ করলে ক্যালকুলেটর খোলে, মান দিলে ফলাফল লাইভ আপডেট হয়। উপরে সার্চ বক্স দিয়ে নাম লিখে সরাসরি সূত্র খুঁজে নেওয়া যায়।

## ব্যবহার
ব্রাউজারে `index.html` খুলুন — আর কিছু লাগবে না।

## GitHub Pages-এ ডিপ্লয়
1. নতুন রিপোজিটরি বানিয়ে এই সব ফাইল রুটে আপলোড করুন: `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`, `README.md`
2. **Settings → Pages** এ যান
3. Branch: `main`, ফোল্ডার `/ (root)` সিলেক্ট করে Save করুন
4. কিছুক্ষণ পর `https://<username>.github.io/<repo-name>/` লিংকে লাইভ হবে

## মোবাইল থেকে ইনস্টল করতে চাইলে
লিংক Chrome-এ খুলে "Add to Home Screen" করুন (এটা PWA, অফলাইনেও কাজ করবে)।

## মেনু ও যোগাযোগ পেজ
উপরে ডানদিকে ☰ বাটনে ট্যাপ করলে একটা সাইড মেনু খোলে, যেখানে আছে:
- ফরমুলা হ্যান্ডবুক (এই পেজ)
- প্রোডাকশন কাউন্টার ক্যালকুলেটর (আগের রিপোর লাইভ লিংক)
- কাউন্টার ক্যালকুলেটর APK ডাউনলোড (Google Drive লিংক)
- যোগাযোগ পেজ (`contact.html`) — ফোন, WhatsApp, Messenger

নতুন আরও অ্যাপ যুক্ত করতে চাইলে `index.html` ও `contact.html` — দুই জায়গাতেই `<nav class="drawer">` ব্লকে একটা নতুন `<a>` লাইন যুক্ত করুন।

## ফাইল গঠন
```
.
├── index.html      # ফরমুলা হ্যান্ডবুক (UI + ৩২টি সূত্রের লজিক)
├── contact.html    # যোগাযোগ পেজ
├── style.css       # সব পেজের শেয়ার্ড স্টাইল
├── manifest.json   # PWA ম্যানিফেস্ট
├── sw.js           # সার্ভিস ওয়ার্কার (অফলাইন ক্যাশিং)
├── icon-192.png
├── icon-512.png
└── README.md
```

## নতুন সূত্র যুক্ত করতে চাইলে
`index.html`-এর ভেতরে `FORMULAS` অ্যারেতে নতুন একটা অবজেক্ট যুক্ত করুন এই প্যাটার্নে:
```js
{ id:'uniqueId', cat:'weight', name:'নাম',
  formula:'প্রদর্শনের জন্য সূত্র',
  inputs:[ {id:'x', label:'লেবেল', unit:'একক', def:10} ],
  calc:(v)=>({ value: v.x * 2, unit:'কিছু' }) }
```
`cat` হতে হবে: `weight`, `yarn`, `machine`, `production`, অথবা `quality` — এর কোনো একটা।
