"# Smart_Disaster_Mangement_System"
# نظام إدارة الكوارث (Disaster Management System)

مختصر سريع:
مشروع قاعدة بيانات باستخدام Oracle SQL/PLSQL لإدارة الكوارث.  
يشمل جداول مترابطة، تريجرات ذكية، حزمة PL/SQL (Procedure + Function)، إدخالات بيانات، واستعلامات تحليلية.  
 حصل المشروع على المركز الثالث بين 600 مشارك، وجائزة Google AI Pro لمدة سنة.

---

# فكرة المشروع
يهدف المشروع إلى بناء قاعدة بيانات منهجية لإدارة عمليات الاستجابة للكوارث، بحيث:
- يتم تسجيل كل كارثة مع موقعها وحالتها.
- تخصيص الفرق الميدانية لكل كارثة.
- متابعة الضحايا وحالتهم (مصاب، متوفى، مفقود...).
- إدارة الأدوات ووسائل التواصل الخاصة بالفرق.
- ضمان أن القواعد (Business Rules) تُطبّق تلقائيًا عبر التريجرات.

---

# بنية المشروع
- DDL/ → أوامر إنشاء الجداول + القيود.  
- Triggers/ → التريجرات الخاصة بتحديث الحالات والتحقق من القواعد.  
- Package/ → الحزمة (Procedures + Functions).  
- Data/ → بيانات أولية (إدخال سجلات).  
- Queries/ → استعلامات تحليلية وتقارير.  
- docs/ → صورة ERD.

---

##  أهم المكونات

### الجداول الرئيسية
- Disasters → لتخزين معلومات الكوارث.  
- Locations → مواقع الكوارث.  
- Victims → الضحايا المرتبطين بكل كارثة.  
- Teams → الفرق الميدانية.  
- Team_Assignment → تخصيص الفرق للكوارث.  
- Equipment → الأدوات المستخدمة.  
- Team_Contact_Phone / Team_Contact_Email → وسائل التواصل.  

### التريجرات
- توليد المفاتيح الأساسية تلقائيًا عبر sequences.  
- تحديث حالة الكارثة إلى "منتهية" عند إدخال وقت الانتهاء.  
- منع تخصيص فريق لكارثة منتهية أو إذا كان الفريق مشغول.  
 

### الحزمة (Package)
-Function COUNT_TEAMS → عدد الفرق المخصصه لكل كارثه.  
- Function COUNT_VICTIMS → حساب عدد الضحايا لكارثة.  

---

###استعلامات ذكية
`sql
-- عرض الكوارث مع مواقعها وحالتها
-- هذا الاستعلام يعرض اسماء الكوارث و اسم الموقع و حالة الكارثة
SELECT DIS.NAME AS "NAME DISASTER", LOC.NAME AS "DISASTER LOCATION", DIS.STATUS AS "DISASTER STATUS" 
FROM DISASTERS DIS INNER JOIN LOCATIONS LOC
ON DIS.DISASTER_ID = LOC.DISASTER_ID;

--  هنا تنفيذ للدوال الموجودة في الحزمة والتي تعرض 
-- عدد الفرق المشاركة في كارثه معينه و عدد الضحايا المتأثرة في كارثة معينه 
BEGIN
DBMS_OUTPUT.PUT_LINE(COUNT_VICTIMS_AND_TEAMS.COUNT_TEAMS(1));
DBMS_OUTPUT.PUT_LINE(COUNT_VICTIMS_AND_TEAMS.COUNT_VICTIMS(1));
END;

### الانجاز:
. المركز الثالث في فعالية (600 مشارك).
. جائزة اشتراك Google AI Pro لمدة سنة.
