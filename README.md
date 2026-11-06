# شوب جنوب سينا: تشغيل المتجر ولوحة الأدمن

الملفات: `index.html` المتجر، `admin.html` لوحة الأدمن، `firebase-config.js` بيانات مشروعك، `firestore.rules` قواعد الأمان.

## 1) إنشاء مشروع Firebase (مجاني)
1. ادخل console.firebase.google.com وأنشئ مشروع جديد.
2. من Project settings أضف تطبيق ويب (`</>`) وانسخ بيانات الإعداد في `firebase-config.js`.

## 2) قاعدة البيانات وقواعد الأمان
1. Build > Firestore Database > Create database (اختار production mode).
2. افتح تبويب Rules، وفي `firestore.rules` غيّر `YOUR_ADMIN_EMAIL@example.com` لإيميلك، والصق المحتوى كله واضغط Publish.

## 3) باسورد الأدمن
1. Build > Authentication > Get started > فعّل Email/Password.
2. تبويب Users > Add user: اكتب إيميلك وباسورد قوي. نفس الإيميل ده اللي في القواعد.
3. لتغيير الباسورد بعدين: Users > ⋮ بجانب حسابك > Reset password.
4. لوحة الأدمن على `/admin.html`. من غير الإيميل والباسورد دول محدش يقرأ الطلبات ولا يعدّل المنتجات، حتى لو فتح الكود.

## 4) النشر على دومين
بـ Firebase Hosting:
```
npm install -g firebase-tools
firebase login
firebase init hosting   # اختار مشروعك، والمجلد "."، وارفض single-page app
firebase deploy
```
هيدّيك لينك `https://اسم-مشروعك.web.app`. تقدر تربط دومينك من Hosting > Add custom domain. يمكن كمان رفع المجلد على Netlify بالسحب والإفلات، لكن لازم تضيف الدومين في Authentication > Settings > Authorized domains.

## 5) أول استخدام
افتح `/admin.html` وادخل. من تبويب المنتجات اضغط "رفع المنتجات التجريبية" أو أضف منتجاتك. أول ما تضيف منتج المتجر يعرض منتجاتك بدل التجريبية.
اتأكد من التحويل في المحفظة أو إنستا باي قبل ما تغيّر حالة الطلب لـ"تم التأكيد". وغيّر رقم المحفظة وعنوان إنستا باي في `index.html` (ابحث عن `WALLET` و`INSTA`).

## 6) تحويله APK
1. بعد ما الموقع يشتغل على لينك https، ادخل pwabuilder.com والصق اللينك.
2. اختار Android > Package for stores وحمّل الملف. فيه APK للتجربة والتوزيع المباشر، وAAB لـGoogle Play.
3. احتفظ بملف مفتاح التوقيع (signing key) وباسورده في مكان آمن، من غيره مش هتقدر تحدّث التطبيق.
4. التحديثات: لما تعدّل الموقع وتنشره، التطبيق بيعرضها لوحده من غير APK جديد.

## ملاحظات
- مفتاح Firebase في `firebase-config.js` ظاهر لأي حد، وده طبيعي. الحماية الفعلية من قواعد Firestore.
- لو لسه ما حطيتش بيانات Firebase، المتجر بيشتغل بمنتجات تجريبية والطلبات مش بتتحفظ.
