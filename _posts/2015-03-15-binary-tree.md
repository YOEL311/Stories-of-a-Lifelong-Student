---
title: עץ בינארי (Binary Tree)
author: nirgn
layout: post
summary: "עץ בינארי הוא מבנה נתונים מופשט, הבנוי / מאורגן בצורת עץ, כשלכל קודקוד יש לכל היותר שני בנים (המתייחסים אליהם כ’בן ימיני’ ו’בן שמאלי’) ולכל קודקוד (פרט לראשון, הנקרא שורש) יש אב יחיד."
category: Data Structures
---

<div class="left">
  <img src="/images/posts/binary-tree/Example_1.png" alt="First example of binary tree" style="width: 20%;">
</div>

עץ בינארי הוא מבנה נתונים מופשט, הבנוי / מאורגן בצורת עץ, כשלכל קודקוד יש לכל היותר שני בנים (המתייחסים אליהם כ'בן ימיני' ו'בן שמאלי') ולכל קודקוד (פרט לראשון, הנקרא שורש) יש אב יחיד. העץ הינו מכוון ז"א שישנו כיוון אחד (במקרה שלנו נראה כמו מלמעלה למטה, כאילו אנו יורדים במורד העץ), וזה מתבטא בכך שכל צומת שומר אך ורק את הבנים שלו ולא את האב.

<!--more-->

עץ הוא בעצם סוג של גרף (מבנה נתונים נוסף, עליו נדבר בעתיד), למי שכן קצת מכיר גרפים אז עץ הוא גרף קשיר ללא מעגלים. עץ בינארי לעומת זאת (מבנה נתונים ספציפי יותר) הוא עץ מכוון (ז"א שניתן ללכת בו בכיוון אחד בלבד, כך שאנו יודעים מי האב ומי הבן), לכל צומת יש יש לכל היותר שני צאצאים (צמתים), וקיים קודקוד אחד ויחיד (שיקרא שורש העץ).

&nbsp;

אבות ובנים בעץ בינארי מוגדרים כאשר יש קשת מ A ל B. זה אומר ש A הוא אב של B ו B הוא בן של A. ניתן לראות בשתי התמונות למטה דוגמאות של עצים בינארים: הימינית עם אותיות, בה ניתן לראות ש A הוא השורש ו B ו C הם הבנים שלו (וכך הלאה), והשמאלית עם מספרים, בה ניתן לראות ש 1 הוא השורש ו 2 ו 3 הם הבנים שלו (וכך הלאה).

<div class="left">
  <img src="/images/posts/binary-tree/Example_2.png" alt="Second example of binary tree" style="width: 20%;">
</div>

&nbsp;

בנוסף, גם לעץ בינארי יש כמה סוגים (מבני נתונים ספציפיים יותר) להלן כמה מהם:

  * **עץ בינארי מלא &#8211;** עץ בו לכל צומת שאינו עלה יש שני בנים.
  * **עץ בינארי מאוזן &#8211;** עץ בו ההפרש בין הגובה של שני תתי-עצים של אותה הצומת לעולם אינו גדול מאחד. לכן הגובה שלו יהיה חסום (מלמעלה) ע"י הערך (log2(n (כאשר n הוא מס' הצמתים בעץ).
  * **עץ בינארי מנוון &#8211;** עץ בו לכל צומת שאינו עלה יש בן אחד בלבד.
  * **עץ חיפוש בינארי &#8211;** בו לכל קודקוד שני בנים. הבן השמאלי (יחד עם כל צאצאיו) קודם לאביו ביחס הסדר, ואילו הבן השמאלי (יחד עם כל צאצאיו) נמצא אחרי אביו מבחינת הסדר.
  * **עץ אדום שחור &#8211;** מבנה נתונים המשלב עץ חיפוש בינארי, עם עץ בינארי מאוזן.

יש לציין כי הפעולות המתבצעות על עצים בינארים נעשות בזמן הנמצא ביחס ישיר לגבוהו של העץ. ובפוסט הזה אנו נתמקד בעץ חיפוש בינארי, ובעץ בינארי מאוזן &#8211; AVL בלבד.

&nbsp;

### Binary Search Tree - עץ חיפוש בינארי

עץ חיפוש בינארי הוא עץ הנתונים הפופלרי ביותר. כל צומת בעץ חיפוש בינארי מכיל את השדות left (הבן השמאלי), right (הבן הימני), p (האב של צומת זו), ואם אחד הבנים או האב חסר, השדה המתאים מכיל את הערך NIL (צומת השורש, הוא הצומת היחיד בעץ ששדה האב שלו מכיל NIL).

על מנת שעץ בינארי יחשב לעץ חיפוש בינארי, על המפתחות בעץ להיות מאוחסנים תמיד באופן כזה שיקיים את תכונת עץ החיפוש הבינארי:

> _יהי x צומת בעץ חיפוש בינארי. אם y הוא צומת בתת עץ השמאלי של x, אזי [key[y] <= key[x. אם y הוא צומת בתת עץ הימיני של x, אזי [key[x] <= key[y._

תכונה זו של עץ החיפוש הבינארי מאפשרת לנו להדפיס בסדר ממוין את כל המפתחות שעץ החיפוש הבינארי מכיל, באמצעות אלגוריתם רקורסיבי פשוט הנקרא סריקה תוכית של עץ (InOrder Tree Walk). שמו של האלגוריתם נגזר מכך שהמפתח של השורש של תת עץ מודפיס בין הערכים המופיעים בתת עץ השמאלי שלו לאלה המופיעים בתת עץ הימיני שלו (בצורה דומה לסריקה תוכית, ישנה גם סריקה תחילת של העץ (PreOrder Tree Walk) המדפיסה את השורש לפני הערכים המופיעים בכל אחד מהתת עצים שלו, וסריקה סופית של העץ (PostOrder Tree Walk) המדפיסה את השורש אחרי הערכים המופיעים בכל אחד מהתת עצים שלו).

להלן Inorder Tree Walk המדפיסה את כל המפתחות בסדר ממוין, בעץ חיפוש בינארי.  
קוד:

```c
INORDER-TREE-WALK (x)
if (x != NIL)
    INORDER-TREE-WALK (left[x])
    print key[x]
    INORDER-TREE-WALK (right[x])
```

 לדוגמה, סריקה תוכית של העץ בתמונה למעלה (השמאלית) תדפיס: 6,3,8,5,7,1,4,2. הסריקה עצמה מתבצעת בזמן (O(n (לעץ בעל n צמתים), שכן לאחר הקריאה ההתחלתית, האלגוריתם נקרא באופן רקורסיבי בדיוק פעמיים עבור כל צומת בעת (פעם בנו השמאלי, ופעם בנו הימיני).

&nbsp;

### שאילתות

אחת הפעולות השכיחות על עץ חיפוש בינארי היא חיפוש מפתח המאוחסן בעץ. מלבד הפעולה Search, עץ חיפוש בינארי יכול לתמוך בשאילתות נוספות (כמו Minimum, Maximum, Successor ו Predecessor). לכן נממשן על עץ חיפוש בינארי בגובה h [בזמן (O(h]. כמו בכל פוסט, הקוד יכתב ב [פסאודו קוד](http://en.wikipedia.org/wiki/Pseudocode).

**Tree-Search -** מחזיר מצביע לצומת בעל מפתח k, אם קיים כזה. אחרת מחזירה NIL.  
קוד:

```c
TREE-SEARCH (x, k)
if (x = NIL or k = key[x])
    return x
if (k < key[x])
    return TREE-SEARCH (left[x], k)
else return TREE-SEARCH (right[x], k)
```

האלגוריתם מתחיל את החיפוש בשורש העץ וסורק מסלול במוקד העץ. בכל צומת x כשהוא נתקל בו, הוא משווה את המפתח k עם [key[x. אם שני המפתחות שווים, החיפוש מסתיים. אם k קטן מ [key[x, החיפוש נמשך בתת עץ השמאלי של x (שכן מתכונת עץ החיפוש בינארי אנו יודעים ש k אינו יכול להימצא בתת עץ הימיני). בדומה, אם k גדול מ [key[x החיפוש נמשך בתת עץ הימיני. הצמתים הנבחנים (כל ה [key[x-ים הנבחנים במהלך הריצה של האלגו') יוצרים מעין מסלול במורד העץ, החל מהשורש שנבחן ראשון. ומכאן שזמן הריצה של האלגו' הוא (O(h, כאשר h הוא גובה העץ.

&nbsp;

**Tree-Minimum -** מחזיר מצביע לאיבר המינימלי.
קוד:

```c
TREE-MINIMUM (x)
while (left[x] != NIL) do
    x <- left[x]
return x
```

 אפשר תמיד למצוא את האיבר בעל המפתח המינימלי בעץ חיפוש בינארי על ידי מעקב אחר המצביעים left, החל משורש העץ ועד שנתקלים ב NIL. הרי תוכנת העץ הבינארי מבטיחה לנו כי הבן השמאלי תמיד יהיה קטן מהעלה הנוכחי ומהבן הימיני שלו (במידה וקיים). לכן נלך שמאלה עד שלא יהיו עוד עלים. אם לצומת אין תת עץ שמאלי, אז המפתח המינימלי בתת עץ המורש ב x הוא השורש עצמו, ז"א [key[x (לכן נחזיר x לא קשר לנעשה בלולאה). אך אם לצומת x יש תת עץ שמאלי, אז כמו שאמרנו לא יכול להיות מפתח בתת עץ הימיני שהוא קטן מ [key[x, וכל המפתחות בתת עץ השמאלי אינם גודלים מ [key[x, לכן המפתח המינימלי יימצא בתת עץ המורש ב [left[x.

&nbsp;

**Tree-Maximum -** מחזיר מצביע לאיבר המקסימלי.
קוד:

```c
TREE-MAXIMUM (x)
while (right[x] != NIL) do
    x <- right[x]
return x
```

 הקוד למציאת האיבר המקסימלי סימטרי לקוד המחזיר מצביע לאיבר המינימלי. הרי מאותה התכונה של עץ בינארי מובטח לנו כי האיבר בעל הערך הגדול תמיד ימצא בתת עץ הימיני (בתת עץ הנגזר מהבן הימיני), לכן נלך ימינה עד אשר נמצא את העלה האחרון (נקבל NIL ואז נדע שהעלה שלפניו הוא העלה האחרון). זמן הריצה של האלגוריתמים למציאת האיבר המינמלי או המקסימלי הוא (O(h, כאשר h הוא גובה העץ (שכן שתי האלגו' סורקים מסלולים במורד העץ).

&nbsp;

**Tree-Successor -** מחזיר את העוקב (הצומת בעל המפתח הקטן ביותר הגדול מ [key[x) לצומת x, אם קיים כזה, ו NIL אם x הוא בעל המפתח הגדול ביותר בעץ.
קוד:

```c
TREE-SUCCESSOR (x)
if (right[x] != NIL)
    return TREE-MINMUM (right[x])
y <- p[x]
while (y != NIL and x = right[y]) do
    x <- y
    y <- p[y]
return y
```

כמו שניתן לראות, הקוד מחולק ל-2 מקרים. אם התת עץ הימיני של צומת x אינו ריק, אז העוקב לx הוא פשוט הצומת השמאלי ביותר (עם הערך הקטן ביותר) בתת עץ הימיני, לכן קוראים ל Tree-Minimum על [right[x. אך במקרה השני בו תת העץ הימיני של צומת x ריק ול x יש עוקב (נקרא לו y). אז y הוא האב הקדמון הנמוך ביותר של x (ז"א הגבוה ביותר בעץ) אשר הבן השמאלי שלו גם הוא אב קדמון של x (שניתן להגיע ממנו ל x אך ורק ע"י ירידה במורד העץ). כדי למצוא את y נעלה בעץ החל מ x עד שנתקל בצומת שהוא הבן השמאלי של אביו (שמתבצע בשורות 4-8 באלגו').

האלגו' Tree-Successor מחזיר את הקודם לצומת x, והינו סימטרי לאגו' הזה. שתיהם רצים בזמן (O(h על עץ בגובה h.

&nbsp;

**Tree-Insert -** כדי להכניס ערך חדש v, לעץ חיפוש בינארי T.
קוד:

```c
TREE-INSERT (T, z)
y <- NIL
x <- root[T]
while (x != NIL) do
    y <- x
    if (key[z] <- key[x])
        x <- left[x]
    else x <- right[x]
p[z] <- y
if (y = NIL)
    root[T] <- z
else if (key[z] <- key[y])
    left[y] <- z
else right[y] <- z
```

 האלגוריתם מקבל כפרמטר צומת z, שעבורו key[z] = v, והבן השמאלי והימיני שלו ריקים (right[z] = NIL ו left[z] = NIL). האלגו' משנה את T וחלק מהשדות של z באופן כזה ש z מוכנס למקומו המתאים בעץ.

האלגו' מתחיל בשורש העץ וסורק מסלול כלפי מטה. המצביע x סורק את המסלול, ו y מצביע תמיד על האב של x (כדי לדעת אחרי איזה איבר להכניס את z). לאחר פעולת האתחול, לולאת ה while בשורות 4-8 גורמת לכך ששני המצביעים (x ו y) ירדו במורד העץ ויפנו שמאלה או ימינה בכל צומת, על פי תוצאת ההשוואה בין [key[z ל [key[x, עד ש x יקבל את הערך NIL ויצא מהלולאה. הערך NIL נמצא בדיוק במיקום בו אני רוצים להציב את איבר הקלט z, ובשורות 9-14 נקבעים ערכי המצביעים הגורמים להכנסתו של z לעץ.

גם כאן, בדומה לפעולות הבסיסיות האחרות על עצי חיפוש בינאריים, האלגו' רץ בזמן (O(h על עץ בגובה h.

&nbsp;

**Tree-Delete -** כדי למחוק צומת נתון z מעץ חיפוש בינארי (המתודה מקבלת מצביע ל z).
קוד:

```c
TREE-DELETE (T. z)
if (left[z] = NIL or right[z] = NIL)
    y <- z
else y <- TREE-SUCCESSOR(z)
if (left[y] != NIL)
    x <- left[y]
else x <- right[y]
if (x != NIL)
    p[x] <- [y]
if (p[y] = NIL)
    root[t] <- x
else if (y = left[p[y]])
    left[p[y]] <- x
    else right[p[y]] <- x
if (y != z)
    key[z] <- key[y]
    copy y-s satellite data into z
return y
```

 פעולת המחיקה קצת יותר מסובכת מכיוון שהיא גורמת לשינוי בקבוצה הדינמית המיוצגת על ידי עץ החיפוש הבינארי. יש לשנות את מבנה הנתונים כך שישקף את השינוי הזה, ויש לעשות זאת בלי להפר את תכונות עץ החיפוש הבינארי.

השגרה מטפלת ב-3 מקרים: אם ל z אין בנים, משנים את אביו [p[z כך שבנו יהיה NIL במקום z. אם לצומת יש רק בן אחד, מסירים את z ע"י יצרת קשר חדש בין אביו לבנו. ואם לצומת יש שני בנים, מסירים את y, העוקב של z אשר לו אין בן שמאלי והמפתח והנתונים הנלווים של z מוחלפים באלה של y. למטה  מצד שמאל, ניתן לראות דוגמה לשלושת המקרים (על פי הסדר שתיארנו כאן).

<div style="text-align: center;">
  <img src="/images/posts/binary-tree/Tree-Delete.png" alt="Delete from Tree">
</div>

בשורות 2-4 האלגוריתם קובע איזה צומת y תוסר. הצומת y היא צומת הקלט z (אם ל z לכל היותר בן אחד) או העוקב של z (אם ל z שני בנים). לאחר מכן, בשורות 5-7, מציבים ב x מצביע לבנו של y שאינו NIL, אם יש כזה, ואם ל y אין בנים מציבים ב x את NIL. בשורות 8-14 מסירים את הצומת y באמצעות שינוי ערכי מצביעים ב [p[y וב x. הסרתו של y מסתבכת קצת עקב הצורך לטפל במקרי קצה בהם x=NIL או y הוא שורש העץ. ולבסוף, אם הצומת שהוסרה הייתה העוקב של z, מעבירים בשורות 15-17 את המפתח ואת הנתונים הנלווים של y אל z במקום המפתח והנתונים הנלווים הקודמים. בשורה 18 מחזירים את הצומת y למתודה הקוראת, כדי שזו תוכל למחזר אותו באמצעות רשימת הפנויים.

זמן הריצה הוא (O(h עבור עץ בגובה h. 

&nbsp;

### לסיכום

אז הצגנו את תכונותיהם הבסיסיות של עצי חיפוש בינאריים, ולאחר מכן ראינו כיצד סורקים עץ חיפוש בינארי כדי להדפיס את ערכיו בסדר ממוין, כיצד מחפשים ערך בעץ חיפוש בינארי, כיצד מוצאים את איבר המינימום או המקסימום, כיצד מוצאים את האיבר העוקב לאיבר נתון (ובאופן סימטרי את האיבר הקודם לאיבר נתון), וכיצד מכניסים איבר לעץ חיפוש בינארי או מוחקים ממנו איבר.

היתרון בעצי חיפוש בינאריים הוא האפשרות לחפש איבר מסוים או למיין את האיברים בזמן מהיר יחסית (לדוגמה ביחס למערך או רשימה מקושרת). הפעולות הבסיסיות שתיארנו יתבצעו במהירות אם עץ החיפוש הוא נמוך, אך אם הוא גבוה, הביצועים לא יהיו טובים יותר מאשר מימוש באמצעות רשימה מקושרת. לכן בפוסט הבא נדבר על עצי חיפוש מאוזנים, או AVL.
