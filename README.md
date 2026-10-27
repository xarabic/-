# SEVANT Browser — دليل الإعداد والنشر من هاتف Android

## ما الذي يعمل في النسخة؟
- واجهة عربية متجاوبة.
- البحث عبر Google وفتح روابط HTTP/HTTPS في تبويب جديد.
- اختصارات Google وYouTube وTikTok وGmail.
- مفضلة وسجل محليان على الجهاز (localStorage).
- تسجيل دخول Google عبر Firebase Authentication بعد إدخال إعدادات مشروعك.

## حدود مهمة
هذا **موقع ويب** وليس محرك متصفح مستقلًا مثل Chrome. لا يستطيع موقع عادي عرض كل المواقع داخله أو مشاركة جلسات تسجيل الدخول معها. الروابط تُفتح في تبويب جديد للمتصفح الحالي. بعض المواقع تمنع التضمين داخل صفحات أخرى. المفضلة والسجل في هذه النسخة محليان على الجهاز ولا تتم مزامنتهما مع حساب Google.

## 1) إنشاء Firebase (مجاني ضمن حدود الخطة المجانية)
1. افتح https://console.firebase.google.com/ من هاتفك وسجّل الدخول.
2. أنشئ مشروعًا باسم `SEVANT Browser`.
3. أضف تطبيق Web (رمز `</>`)، وسجّل اسمًا مثل `sev-browser`.
4. انسخ إعدادات Firebase الخاصة بتطبيق الويب.
5. من Authentication > Get started > Sign-in method فعّل Google، واختر بريد دعم المشروع واحفظ.
6. من Authentication > Settings > Authorized domains أضف نطاق Vercel بعد نشر الموقع، مثل `your-project.vercel.app` (لا تكتب https://).
7. افتح `firebase-config.js` واستبدل `YOUR_FIREBASE_API_KEY` و`YOUR_PROJECT_ID` و`YOUR_FIREBASE_APP_ID` بالقيم الحقيقية من إعدادات تطبيق الويب. اترك `authDomain` كما ورد في Firebase إن كان مختلفًا.
8. إعداد Firebase Web config ليس كلمة مرور سرية، لكن يجب حماية قواعد أي قواعد بيانات مستقبلية. هذا المشروع لا يستخدم قاعدة بيانات.

## 2) النشر على Vercel من الهاتف
1. فك ضغط ZIP على هاتفك باستخدام مدير الملفات.
2. أنشئ مستودعًا جديدًا في GitHub إن كان حسابك يعمل، وارفع الملفات الثلاثة: `index.html` و`firebase-config.js` و`README.md` إلى جذر المستودع. أو استخدم طريقة استيراد مشروع Git المتاحة في Vercel.
3. افتح https://vercel.com/new وسجّل الدخول.
4. استورد المستودع. لأنه موقع ثابت، لا تحتاج إلى Build Command أو Output Directory خاصين؛ اترك الإعدادات الافتراضية إذا كان Vercel يتعرف على المشروع كصفحات ثابتة.
5. انشر المشروع، ثم انسخ رابط `*.vercel.app`.
6. أضف نطاق Vercel إلى Firebase Authentication > Settings > Authorized domains.
7. افتح الموقع من رابط Vercel واختبر زر الدخول.

## 3) الاختبار
- جرّب كتابة `youtube.com` واضغط «اذهب».
- جرّب عبارة بحث مثل `أخبار اليوم`.
- أضف `https://example.com` إلى المفضلة.
- اختبر تسجيل Google بعد إكمال إعداد Firebase والنطاقات.
- إذا ظهر `auth/unauthorized-domain`، أضف نطاق Vercel إلى Authorized domains.
- إذا ظهر خطأ في تسجيل Google، تحقق أن Google مفعّل في Sign-in method وأن إعدادات Firebase صحيحة.

## الأمان
- لا تطلب كلمة مرور Google داخل صفحة SEVANT.
- لا تضع مفاتيح Admin SDK أو service-account JSON أو أسرار الخادم في ملفات الواجهة.
- لا تدّع أن المستخدم دخل إلى موقع خارجي؛ تسجيل الدخول هنا يخص SEVANT فقط.
