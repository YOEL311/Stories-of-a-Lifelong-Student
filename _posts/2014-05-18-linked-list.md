---
title: רשימה מקושרת (Linked List)
author: nirgn
layout: post
summary: "רשימה מקושרת היא מבנה נתונים שבו העצמים ערוכים בסדר לינארי. אולם בניגוד למערך, שבו הסדר הלינארי נקבע על ידי אינדקסים, ברשימה מקושרת הסדר נקבע על ידי מצביעים הכלולים בכל אחד מן העצמים."
category: Data Structures
---
רשימה מקושרת היא מבנה נתונים שבו העצמים ערוכים בסדר לינארי. אולם בניגוד למערך, שבו הסדר הלינארי נקבע ע"י אינדקסים, ברשימה מקושרת הסדר נקבע ע"י מצביעים הכלולים בכל אחד מן העצמים.

<!--more-->

באמצעות רשימה מקושרת ניתן לייצא קבוצות דינמיות באופן פשוט וגמיש (אם כי לא בהכרח ביעילות). רשימה יכולה להיות חד-מקושרת או דו-מקושרת, ממוינת או לא ממוינת, מעגלית או לא מעגלית.
ברשימה חד מקושרת (singly linked) האיברים אינם מכילים את השדה prev.
ברשימה ממוינת (sorted), הסדר הלינארי של איברי הרשימה מתאים לסדר הלינארי של המפתחות המאוחסנים בהם, איבר המינימום הוא ראש הרשימה ואיבר המקסימום הוא הזנב.
ברשימה בלתי ממוינת (unsorted), האיברים מופיעים בסדר כלשהו.
ברשימה מעגלית (circular list), המצביע prev של ראש הרשימה מצביע על זנבה, והמצביע next של זנב הרשימה מצביע על ראשה. רשימה כזו ניתן לראות כמעגל של איברים.

כפי שניתן לראות בתמונה למטה, L הוא עצם המכיל שדה מפתח key ושני שדות נוספים של מצביעים: next ו prev. בהינתן איבר x ברשימה, `[next[x` מצביע על האיבר העוקב לו ברשימה המקושרת, ו `[prev[x` מצביע על האיבר הקודם לו. אם `prev[x] = NIL`, אין ברשימה איבר עוקב ל x (ז"א שהוא האיבר האחרון, או זנב (tail) הרשימה). באותו אופן `[head[L` מצביע על האיבר הראשון ברשימה. אם `head[L] = NIL`, הרשימה ריקה.


ב (i) אנו רואים רשימה דו מקושרת L המייצגת את הקבוצה {16 ,9 ,4 ,1}. כל איבר ברשימה הוא עצם בעל שדה מפתח ושדות מצביעים (המיוצגים כאן ע"י חיצים) לעצם הבא (next) ולעצם הקודם (prev). השדה next של זנב הרשימה והשדה prev של ראש הרשימה - ערכם NIL (במיוצג כאן ע"י אלכסון), ו `[head[L` מצביע על ראש הרשימה. השלב השני (ii) הוא לאחר ביצע `(LIST-INSERT(L, x`, כאשר `key[x] = 25`, לכן כעת העצם החדש בעל ערך המפתח 25 נמצא בראש הרשימה. העצם החדש של ראש הרשימה (25) מצביע על ראש הרשימה הקודם (שהמפתח שלו 9). והשלב השלישי (iii) הוא לאחר קריאה ל `(LIST-DELETE(L, x`, כאשר x מצביע על עצם אשר המפתח שלו הוא 4.

&nbsp;

**חיפוש ברשימה מקושרת**

השגרה מוצאת את האיבר הראשון בעל המפתח k ברשימה L באמצעות חיפוש לינארי פשוט, ומחזירה מצביע לאיבר זה (אם אינה מוצאת ברשימה איבר בעל המפתח k, היא מחזירה NIL).

```c
LIST-SEARCH (L, k)
x <- head[L]
while (x != NIL and key[x] != k) do
     x <- next[x]
return x
```
זמן הריצה (O(n.

&nbsp;

**הכנסה לרשימה מקושרת**

בהינתן איבר x אשר שדה המפתח שלו כבר מכיל ערך, השגרה תכניס אותו לראש הרשימה המקושרת.

```c
LIST-INSERT (L, x)
next[x] <- head[L]
if (head[L] != NIL)
     prev[head[L]] <- x
head[L] <- x
prev[x] <- NIL
```
זמן הריצה (O(1.

&nbsp;

**מחיקה מרשימה מקושרת**

השגרה מוחקת איבר x מהרשימה המקושרת L. היא מקבלת מצביע לx ומסירה אותו באמצעות עדכון מצביעים. מפני שהשגרה מקבלת מצביע ולא האיבר, אם אנו רוצים למחוק ערך נתון, יש קודם לחפשו ברשימה המקושרת (באמצעות השגרה LIST-SEARCH, כדי לקבל מצביע לאותו איבר, ורק לאחר מכן למחוק אותו בעזרת מצביע זה).
> יש לציין כי השגרה מבצעת טיפול מיוחד במקרי הקצה (ראש וזנב הרשימה).

```c
LIST-DELETE (L, x)
if (prev[x] != NIL)
     next[prev[x]] <- next[x]
else head[L] <- next[x]
if (next[x] != NIL)
     prev[next[x]] <- prev[x]
```
זמן הריצה (O(1.

&nbsp;

### זקיפים

זקיף (באנגלית: Sentinel) הוא עצם דמה המאפשר לנו לפשט את הטיפול במקרי הקצה. לדוגמה, נוסיף לרשימה L עצם `[nil[L`, המייצג NIL אולם כולל את כל השדות של איברי הרשימה האחרים. כל התייחסות בקוד לNIL תוחלף בהתייחסות לזקיף `[nil[L`. כפי שנראה באיור שלמטה שינוי זה הופך רשימה דו מקושרת רגילה לרשימה דו מקושרת מעגלית עם זקיף, כאשר הזקיף `[nil[L` מוצב בין ראש הרשימה לבין זנבה.
השדה `[[next[nil[L` מצביע על ראש הרשימה, ו `[[prev[nil[L` מצביע על זנבה. ובאופן דומה השגה next של זנב הרשימה והשדה prev של ראש הרשימה מצביעים שניהם על `[nil[L`. ומכיוון ש `[[next[nil[L` מצביע על ראש הרשימה, נוכל לוותר על המאפיין `[head[L` ולהחליף את ההתייחסות אליו ב `[[next[nil[L`.

&nbsp;

**חיפוש ברשימה מקושרת**

הקוד של LIST-SEARCH אינו משתנה, פרט להתייחסויות ל NIL ול [head[L, שמשנים אותן כמו שתיארנו לעיל.

```c
LIST-SEARCH (L, k)
x <- head[L]
while (x != NIL and key[x] != k) do
     x <- next[x]
return x
```

&nbsp;

**הכנסה לרשימה מקושרת**

```c
LIST-INSERT (L, x)
next[x] <- next[nil[L]]
prev[next[nil[L]] <- x
next[nil[L]] <- x
prev[x] <- nil[L]
```

מחיקה מרשימה מקושרת: הקוד נשאר כשהיה - ללא שינוי.
