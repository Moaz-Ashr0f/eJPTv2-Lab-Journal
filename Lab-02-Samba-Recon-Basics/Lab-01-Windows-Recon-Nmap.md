# 🧪 Lab 01 – Windows Recon: Nmap Host Discovery

![Nmap without Pn](./screenshots/ping+nmap.png)

![Version detection with -sV](./screenshots/services-version-detection.png)



## 🎯 الهدف من اللاب:
استكشاف طرق اكتشاف الأجهزة (Host Discovery) باستخدام أداة Nmap والتعامل مع الحالات اللي بيمنع فيها التارجت الـ ping (ICMP).

## 📌 اللي حصل معايا:
وأنا ببدأ أعمل ping للتارجت لاحظت إنه مش بيرد خالص جربت بعدها أشغل:
```bash
nmap <target>
```

لكن الـ Nmap طلعلي الرسالة دي:
Note: Host seems down. If it is really up, but blocking our ping probes, try -Pn
بدأت أشك إن الجهاز ممكن يكون شغال، بس فيه حاجة بتمنع الـ ping.

🔍 الاستنتاج:

    اكتشفت إن أحيانًا بيكون فيه firewall بيمنع ICMP (وده البروتوكول اللي الـ ping بيعتمد عليه في معرفه هل الجهاز الاخر شغال واقدر اوصل ليه ولا لا ؟)
    
    والـ Nmap بشكل افتراضي بيبعت ping قبل ما يبدأ يفحص البورتات 

    فلو الـ ICMP مش شغال، الـ Nmap هيفتكر إن الجهاز طافي.


  🛠 الحل:

جربت الأمر ده:
```bash
nmap -Pn <target>
```
ال -Pn بيقول للـ Nmap: اعتبر الجهاز شغال وابدأ افحص البورتات من غير ما تتأكد بـ ping

وفعلاً، الـ scan اشتغل وبدأ يطلعلي البورتات المفتوحة.


🔍 كمان:

علشان أتعرف على نوع الخدمات اللي شغالة على البورتات، استخدمت:
```bash
nmap -Pn -sV <target>
```

ال -sV بيخلّي الـ Nmap يحاول يجيب اسم الخدمة والإصدار بتاع الخدمه 

💡 الخلاصة:

    مش كل مرة تشوف "host seems down" تبقى المشكلة من الجهاز.

    الـ firewall ممكن يمنع الـ ping (ICMP).

    استخدم -Pn في الحالات دي.

    ومع -sV هتقدر تعرف الخدمات والنسخ بسهولة.

    

