RANGPUR MARBLE & GRANITE — CLOUD FOUNDATION v3

গুরুত্বপূর্ণ
- এই সংস্করণে Firebase Email/Password signup, login, password reset এবং Firestore member check আছে।
- এটি এখনো পূর্ণ ব্যবসা অ্যাপ নয়; পুরোনো customer/order/sales/stock/finance মডিউল Cloud Firestore-এ sync করে না। বাস্তব হিসাবের ডেটা এখনই দেবেন না।
- কোনো Billing account, payment card বা Blaze upgrade লাগবে না। Firebase Console-এ Spark/No-cost plan-এই থাকুন।
- Firebase free quota/নীতি ভবিষ্যতে বদলাতে পারে; quota ছাড়ালে Spark plan-এ সার্ভিস সীমিত/বন্ধ হতে পারে। 100% free চাহিদার কারণে billing enable করবেন না।

১) index.html Chrome-এ চালু করুন। Firebase SDK লোডের জন্য ইন্টারনেট লাগবে।
২) প্রথমে নিজের ইমেইল দিয়ে New Account তৈরি করুন।
৩) স্ক্রিনে দেখানো Firebase UID কপি করুন।
৪) Firebase Console > Firestore Database > Data-তে গিয়ে নিচের collection/document তৈরি করুন:
   businesses (collection)
     rangpur-marble-granite (document)
       members (subcollection)
         [আপনার Firebase UID] (document ID)
           role: "owner" (string)
           email: "আপনার Firebase login email" (string)
৫) এরপর HTML পেজে ফিরে “অনুমতি আবার পরীক্ষা” চাপুন বা logout/login করুন। Approved দেখালে owner membership ঠিক আছে।
৬) দ্বিতীয় ও তৃতীয় পার্টনারকে তাদের নিজস্ব ইমেইল দিয়ে account তৈরি করতে বলুন। প্রত্যেকের UID একই members subcollection-এ নতুন document ID হিসেবে যোগ করুন, role "partner" এবং email field দিন।

SECURITY RULES
- Firestore > Rules-এ firestore.rules ফাইলের সম্পূর্ণ কোড বসিয়ে Publish করুন।
- এই Rules-এ সদস্যরা কেবল নিজেদের member document পড়তে পারে; client থেকে member তৈরি/পরিবর্তন করতে পারে না।
- ব্যবসার ভবিষ্যৎ ডেটা businesses/rangpur-marble-granite/workspace/ path-এর নিচে রাখতে হবে। অনুমোদিত সদস্যরা সেখানে read/write করতে পারবে।
- কোনো app data অন্য collection/path-এ রাখবেন না, যতক্ষণ না Rules পর্যালোচনা করে আপডেট করা হয়।

নিরাপত্তা
- Google password, email password, OTP, service-account private key কাউকে দেবেন না।
- Firebase Web API key সাধারণত client config-এ থাকে; নিরাপত্তা Firestore Rules ও Auth দিয়ে enforce করতে হবে।
- বাস্তব আর্থিক ব্যবহার শুরুর আগে backup, conflict handling, audit log এবং accounting logic পরীক্ষা করা আবশ্যক।
