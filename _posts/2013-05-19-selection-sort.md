---
title: מיון בחירה (Selection Sort)
author: nirgn
layout: post
summary: "Selection Sort - מיון בחירה, הינו האלגוריתם האינטואיטיבי ביותר (לפחות לפי דעתי). אלגוריתמם זה משתמש במבנה הנתונים הבסיסי והידוע - מערך."
category: Algorithms
---
Selection Sort - מיון בחירה, הינו האלגוריתם האינטואיטיבי ביותר (לפחות לפי דעתי). אלגוריתם זה משתמש במבנה הנתונים הבסיסי והידוע - [מערך]({% post_url 2013-02-17-array %}).

### עקרון האלגוריתם

  * נמצא את האיבר בעל הערך הנמוך ביותר במערך.
  * נחליף אותו עם האיבר הראשון במערך.
  * ונמשיך באותה שיטה על שאר המערך (ללא האיבר הראשון).

<!--more-->

&nbsp;

### הקוד של האלגוריתם ב[פסאודו קוד](http://en.wikipedia.org/wiki/Pseudocode)

```c
SELECTION-SORT(A)
for (i <- 1 to n-1) do
    min <- i
    for (j <- i+1 to n) do
        if (A[min] > A[j])
            min <- j
    exchange A[i] <-> A[min]
```

<div class="left">
  <img src="/images/posts/selection-sort/selection-sort-animation.gif" alt="Selection Sort Animation">
</div>

להלן אנימציה (בצד שמאל) של האלגוריתם בפעולה על מערך, כשהמערך ההתחלתי הוא {7 ,8 ,4 ,1, 3, 9, 6, 2, 5, 8}, והמערך המתקבל בסוף הוא {9, 8 ,7, 6, 5, 4, 3, 2, 1, 0}.

**הסבר מופשט:**

ניתן לראות בקוד שישנה לולאה מקוננת (לולאה בתוך לולאה), על מנת לבדוק מהו האיבר הקטן ביותר במערך ולשים אותו במקום הראשון, ולאחר מכן (באיטצריה השניה של הלולאה החיצונית), שוב, נבדוק מהו האיבר הקטן ביותר במערך אך הפעם זהו יהיה תת מערך - מהאינקס השני ועד ל n (האינדקס האחרון במערך, או גודל המערך) וכך הלאה עד מערך בגודל תא אחד.

בלולאה החיצונית אנו עוברים על המערך מהאיבר הראשון ועד לאיבר הלפני אחרון. אנו מכניסים את האינדקס (שעובדים עליו כעת) למשתנה בשם min, ומתחילים בלולאה הפנימית להשוות אותו לכל האיברים שאחריו ( i+1 ) ועד לאיבר האחרון במערך. אם אנו מוצאים איבר שקטן ממנו נכניס את האינדקס (מספר התא) למשתנה min.

בסיום הריצה של האלגוריתם הפנימי נחליף את המשתנה שמצאנו (המשתנה הכי קטן מתוך סדרת הערכים שבה חיפשנו. שאינה בהכרח כל המערך, ובנוסף הסדרה תקטן בכל איטרציה) במשתנה באינדקס הראשון בתת המערך.

&nbsp;

### הרצה של הקוד לשם המחשה של השלבים המתבצעים

1. נקבל מערך: { 5, 7, 1, 3 }.
2. שורה 2: נתחיל לולאה מהתא הראשון עד לתא הלפני אחרון ונבצע:
  * שורה 3: נכניס את מס' התא (i) למשתנה בשם min (ז"א min מכיל כרגע את המס' 1).
  * שורה 4: ניכנס ללולאה חדשה מהתא ה i+1 (כרגע תא מס' 2) עד לתא האחרון במערך ונבצע:
    * שורה 5: אם הערך בתא מס' min גדול מהערך בתא מס' j שהוא התא הנבדק כרגע).
    * שורה 6: אז נכניס את j ל min (נחליף את מס' התא הקטן ביותר).
  * במעבר הראשון, נראה כי 1 קטן מ 3, ולכן min יהיה שווה 2 (כי הערך 1 נמצא בתא מס' 2), במעבר הבא, 7 גדול מ 1 ולכן לא נבצע דבר, גם 5 גדול מ 1 ולכן לא נבצע דבר.
  * שורה 7: נחליף את האיבר בתא מס' i (שבאיטרציה הזאת, הראשונה, הינו התא הראשון) באיבר שבתא מס' min (שזהו התא בעל האיבר עם הערך הקטן ביותר שמצאנו).
3. כרגע המערך יראה כך: { 5, 7, 3, 1 }.
4. נגיע שוב לשורה 2: הפעם i יעלה ל 2 ונבצע:
  * שורה 3: נכניס את מס' התא (i) למשתנה בשם min (ז"א min מכיל כרגעאת המס' 2).
  * שורה 4: ניכנס ללולאה חדשה מהתא ה i+1 (כרגע תא מס' 3) עד לתא האחרון במערך ונבצע:
    * שורה 5: אם הערך בתא מס' min גדול מהערך בתא מס' j שהוא התא הנבדק כרגע).
    * שורה 6: אז נכניס את j ל min (נחליף את מס' התא הקטן ביותר).
  * מעבר ראשון: 7 לא קטן מ 3 ולכן לא נבצע דבר. מעבר שני: 5 לא קטן מ 3 ולכן לא נבצע דבר.
  * שורה 7: נחליף את האיבר בתא מס' i (שבאיטרציה הזאת, הראשונה, הינו התא הראשון) באיבר שבתא מס' min (שזהו התא בעל האיבר עם הערך הקטן ביותר שמצאנו), ז"א שנחליף את האיבר בתא מס' 3 עם האיבר בתא מס' 3 (נחליף אותו בעצמו).
5. כרגע המערך יראה כך: { 5, 7, 3, 1 }.
6. נגיע שוב לשורה 2: הפעם i יעלה ל 3 ונבצע:
  * שורה 3: נכניס את מס' התא (i) למשתנה בשם min (ז"א min מכיל כרגע את המס' 3).
  * שורה 4: ניכנס ללולאה חדשה מהתא ה i+1 (כרגע תא מס' 4) עד לתא האחרון במערך ונבצע:
    * שורה 5: אם הערך בתא מס' min גדול מהערך בתא מס' j שהוא התא הנבדק כרגע).
    * שורה 6: אז נכניס את j ל min (נחליף את מס' התא הקטן ביותר).
  * מעבר ראשון 5 קטן מ 7 ולכן min יהיה שווה 4 (כי הערך 5 נמצא בתא מס' 4).
  * שורה 7: נחליף את האיבר בתא מס' i (שבאיטרציה הזאת, הראשונה, הינו התא הראשון) באיבר שבתא מס' min (שזהו התא בעל האיבר עם הערך הקטן ביותר שמצאנו).
7. כרגע המערך יראה כך: { 7, 5, 3, 1 }.
8. נגיע שוב לשורה 1: הפעם i יעלה ל 4, אך לא ניכנס שוב ללולאה, מכיוון ש n (מס' התאים במערך) הוא 4, ולפי תנאי הלולאה אנו נכנסים אליה רק כאשר i קטן שווה ל n-1 (שבמקרה שלנו, זה בעצם 3).

**סיבוכיות זמן ריצה: (O(n^2**.  
**סיבוכיות מקום: (O(1**.
