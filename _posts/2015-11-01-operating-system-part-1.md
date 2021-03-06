---
title: 'מערכות הפעלה - חלק 1 (הקדמה)'
author: nirgn
layout: post
summary: פוסט זה הוא הראשון בסדרת פוסטים על מערכות הפעלה, ומהווה הקדמה ויישור קו תיאורטי של הנושא.
base-images-url: 'operating-system-part-1'
category: Operating Systems
---
פוסט זה הוא הראשון בסדרת פוסטים על מערכות הפעלה, ומהווה הקדמה ויישור קו תיאורטי של הנושא. אציין מראש כי הפוסטים בסדרה יהיו כבדים (בעלי מלל רב) וטכניים. הפוסטים נועדו למי שולמד מערכות הפעלה כחלק מתואר במדעי המחשב ו/או למי שמעוניין ללמוד לבד ו/או לאנשים שרק רוצים להיזכר (בראש כל פוסט יהיה תוכן עניינים). 

  1. מהי מערכת ההפעלה
  2. ההיסטוריה של מערכות ההפעלה
  3. גן החיות של מערכות ההפעלה
  4. מושגים בסיסיים
  5. קריאות מערכת
  6. המבנה של מערכות הפעלה

<!--more-->

&nbsp;

### 1. מהי מערכת הפעלה

<img src="/images/posts/operating-system-part-1/os_stack.png" alt="OS Stack">

מערכת הפעלה היא תוכנה שמנהלת את חומרת המחשב. מערכות הפעלה גם מספקות בסיס להרצת אפליקציות שונות ומשמשות תווך בין משתמשי המחשב לבין החומרה (תמונה משמאל). למרות שמערכת ההפעלה משמשת כתווך, אין זה אומר שכל פעולה שאפליקציה או שירות מסוים יבצעו עוברת דרך מערכת ההפעלה (לכן ישנו קו בצד שמאל שמקשר בין האפליקציה ישירות לחומרה). חשבו מה היה קורה אילו כל הוראה של תוכנית משתמש הייתה מצריכה פנייה לממשק המשתמש ומשם לגרעין מערכת ההפעלה (kernel), איזה דיילי ועל כמה משאבים מבוזבזים מדובר. ובמקרים מסויימים, אין צורך אפילו בפנייה לחומרה (לדוג' כאשר תוכנית מסויימת מבקשת לבצע הוראה הדורשת קיום הרשאה מיוחדת, ההרשאה תיתן ע"י מערכת ההפעלה, ללא קשר לחומרה).

החץ מהחומרה אל גרעין המערכת (Kernel) מתייחס למקרים בהן אין צורך בפנייה לחומרה, אך ישנו צורך בפנייה אל ה kernel (כמו שניתן לשים לב, אין חץ ישיר ממלבן האפליקציות אל גרעין המערכת). כאשר הוראות כאלו מגיעות (מכונות גם הוראות מיוחסות) המעבד עובר למצב המכונה מצב מיוחס (kernel mode או supervisor mode), בעוד הוראות שאינן מיוחסות מתבצעות במצב משתמש (user mode), ז"א שהמעבד מספק תמיכה כדי שמערכת ההפעלה תוכל להגן על משאביה. ההגנה מיועדת לחסום את אפשרות ההתערבות של המשתמשים בפעולתה של המערכת עצמה (בפועל, ההבחנה בין מצב מיוחס למצב משתמש נעשית ע"י מידור של קבוצת פקודות מכונה מיוחסות שאינן עומדות לעולם לרשות המשתמש הרגיל).

&nbsp;

**על מערכת ההפעלה ניתן להסתכל מ-2 כיוונים:**

  1. **מלמעלה למטה &#8211;** מכיוון זה, מערכת ההפעלה נראת כמכונה מדומה (או מכונה מורחבת), והינה שכבת תוכנה שנמצאת מעל התוכנה ומתחת ליישומי תוכנה אחרים, ומספקת למשתמש ממשק שמאפשר שימוש בחומרה. בדרך כלל, שכבת תוכנה זו מספקת למשתמש ממשק לחומרה שהינו נוח וקל לתכנות, ובכך מסתירה מהמשתמש את מורכבות הפעולה האמיתית של החומרה.
  2. **מלמטה למעלה &#8211;** מחשב מורכב מרכיבים רבים ושונים. ומנהל המשאבים (כחלק ממערכת ההפעלה כולה) הוא תוכנה שמנהלת את הקצאת המשאבים האלה לתהליכים שרצים במערכות שמעל מערכת ההפעלה.

&nbsp;

### 2. ההיסטוריה של מערכות ההפעלה

<div class="left">
  <img src="/images/posts/operating-system-part-1/punched_cards_programming.jpg" alt="Punched Cards Programming" style="width: 35%">
</div>

במחשבים הראשונים, ללא מערכות ההפעלה, כל תוכנית הייתה צריכה מפרט מלא של החומרה כדי לפעול כראוי ולבצע משימות סטנדרטיות. והמורכבות ההולכת וגדלה של החומרה ושל התוכניות (האפליקציות) הפכו בסופו של דבר את מערכות ההפעלה להכרח. מערכת ההפעלה מספקת סט של פונקציות נחוצות המשמשת את רוב תוכניות המחשב (האפליקציות), ולינקים הדרושים כדי לשלוט ולסנכרן את חומרת המחשב.

המחשבים הראשונים היו מחשבי mainframe (מחשבים מרכזיים חסרי כל צורה של מערכת הפעלה). לכל משתמש היה שימוש בלעדי של המכונה לתקופה קצובה של זמן, והיה מגיע עם התוכנית והנתונים מראש (על [כרטיסי נייר מנוקבים](https://en.wikipedia.org/wiki/Punched_card) וסרטים מגנטיים). התוכנית הייתה נטענת למכונה, והמכונה הייתה מוגדרת לעבוד עד שהתוכנית הושלמה או התרסקה (ניתן היה לדבג, Debugging, באמצעות לוח בקרה עם מתגים ונוריות). עם הזמן חל שינוי משמעותי של ממשק מערכות ההפעלה ובדיוק כמו מכוניות ישנות שהיו חסרות מהירות האצה, מכשיר רדיו, מזגן, וכד' שהפכו אח"כ לסטנדרטיים, כך יותר ויותר מהתוכנות האופציונליות (עורכי טקסט, מנהלי קבצים, דפדפן, וכד') הפכו לסטנדרט בכל חבילה של מערכת הפעלה. אך הצאצא האמיתי של מערכות ההפעלה המוקדמות הוא מה שנקרא היום ליבה / גרעין (kernel).

**מושגים שיש להכיר:**

  * **מערכות אצווה ([Batch System](https://en.wikipedia.org/wiki/Batch_processing)) &#8211;** מערכת שיכולה לבצע באופן רצוף סדרה של משימות שהוכנה מראש. במערכת כזו כל משימה תתבצע מתחילתה ועד סופה (מבלי לשתף את המעבד עם תהליכים אחרים, כפי שנעשה במערכות עם timesharing).
  * **ריבוי תוכניות ([Multiprogramming](https://en.wikipedia.org/wiki/Computer_multitasking#Multiprogramming)) &#8211;** שיטה שבה מס' תהליכים יכולים להימצא בזיכרון הראשון בו זמנית. שיטה זו מייעלת את ניצול המעבד ע"י הקצאתו לתהליך שממתין לו, בזמן שהתהליך שהתבצע קודם ממתין לאירוע כלשהו (למשל קבלת קלט מהאינטרנט).
  * **חלוקת זמן ([Timesharing](https://en.wikipedia.org/wiki/Time-sharing)) &#8211;** שיטה שבה המערכת מאפשרת למספר משתמשים אינטרקטיביים לעבוד בו זמנית, כל אחד מהמסוף שלו (Terminal). בשיטה זו כל משתמש מקבל את הקצאת המעבד לפרק זמן מוגבל כדי לבצע עבודות, וכשהזמן מסתיים ההקצאה עוברת למשתמש אחר. העבודות של המשתמש שממנו נלקח המעבד ממשיכות לרוץ כאשר המשתמש מקבל את המעבד בפעם הבאה.

&nbsp;

### 3. גן החיות של מערכות ההפעלה

במהלך השנים התפתחו סוגים רבים ושונים של מערכות הפעלה, שלכל אחת ייעוד מרכזי משלה. בשנים האחרונות הרבה מסוגים אלו מתמזגים ומתאחדים, בעיקר בגלל ההתקדמות במחשוב האישי. למרות זאת בפסקה זו אציג בקצרה את הסוגים העיקריים של מערכות ההפעלה, גם אם כבר אינן איתנו. להלן הסוגים העיקריים:

  * **מערכות הפעלה למחשב מרכזי (mainframe operating system) &#8211;** מחשב מרכזי הוא מחשב בעל עוצמה חישובית גדולה, המשמש ארגונים גדולים (כגון מוסדות ממשלתיים, חברות מסחריות גדולות, בנקים, אוניברסיטאות וכ'ו) להפעלת יישומים רבים באמצעות עיבוד נתונים רחב היקף (לדוג' מרשם תושבים, תזמון טיסות מטוסים, ביצוע פעולות כספיות, וכל זה תוך כדי שירות משתמשים רבים). מערכות הפעלה למחשבים מרכזיים תוכננו לנצל בצורה יעילה את משאבי המחשב המרכזי, ולספק אמינות ואבטחת מידע גבוהים. הרבה מהרעיונות של מערכות ההפעלה למחשבים מרכזיים מצאו את דרכן, עם הזמן, למערכות הפעלה המשמשות מחשבים אחרים.
  * **מערכות הפעלה לשרתים ([server operating system](http://www.webopedia.com/TERM/S/server_operating_system.html)) &#8211;** שרת מתאפיין בהפעלת מס' רב של תוכניות ותהליכים במקביל. כל תכנית או תהליך משרתים בדרך כלל מספר משתמשי קצה במחשבים המחוברת לשרת אשר ניגשים אל השרת באמצעות רשת האינטרנט. מערכות הפעלה לשרתים שמות דגש על זמינות ושרידות (למשל בשרתי אינטרנט כל נפילה או תקלה בתהליך או ביישום על גבי השרת פירושה השבתת שירות, וזו עלולה לגרום לניתוק ולאי הצגה של אתרי אינטרנט המאוחסנים על השרת). לכן שרתי אינטרנט מסופקים עם רכבי חומרה עודפים שמערכת ההפעלה יכולה לעבוד איתם במקביל, ובמקרה שהרכיב יוצא מכלל פעולה, המערכת תעבור לעבוד במתכונת חירום עם הרכיב העודף. בנוסף, במערכת הפעלה מסוג זה ניתן, לרוב, גם להחליף רכיבים "on the fly".
  * **מערכות הפעלה מקביליות (multiprocessor operating system) &#8211;** מחשב מקבילי הוא מחשב המצויד ביותר ממעבד אחד. המעבדים במחשב מקבילי בדרך כלל חולקים זיכרון ושעון, והתקשורת נעשית לרוב דרך הזיכרון המשותף (ארכיטקטורה כזאת מכונה tightly coupled processors). ניתן להבחין בין 2 סוגים: הראשון עם מעבדים סימטריים (מערכות הפעלה הרצות על מעבדים מסוג זה משתמשות בטכניקה המכונה [Symmetric Multi Processing](https://en.wikipedia.org/wiki/Symmetric_multiprocessing) או בקיצור SMP והן יכולות לרוץ על כל אחד מהמעבדים, תהליכים יכולים להיות מתוזמנים גם על כל אחד מהמעבדים. ומחשבים ביתיים בימנו, שמצוידים ביותר ממעבד אחד, עושים, לרוב, שימוש בטכניקה זו). והשני עם מעבדים אסימטריים (בסוג זה מערכת ההפעלה רצה על מעבד אחד, הנקרא master. שאר המעבדים מכונים slaves ומערכת ההפעלה מקצה להם משימות. מערכות הפעלה מסוג זה נפוצות במחשבים גדולים יותר).
  * **מערכות הפעלה מבוזרות ([distributed operating system](https://en.wikipedia.org/wiki/Distributed_operating_system)) &#8211;** במערכות אלו החישוב מבוזר בין מספר מעבדים כאשר לכל אחד מהמעבדים זיכרון ושעון משלו. מעבדים אלה מכונים loosely coupled processors. המעבדים מתקשרים בינהם דרך קווי תקשורת מסוגים שונים, כמו אפיקים ([buses](https://en.wikipedia.org/wiki/Bus_(computing))) או בתקשורת על גבי רשת לוקאלית. מערכות הפעלה מסוג זה שמות דגש על שיתוף משאבים, אמינות, ביזור עומסים ומאפשרות חישוב מהיר יותר.
  * **מערכות הפעלה למחשבים ביתיים (personal computer operating system) &#8211;** תפקיד מערכות ההפעלה מהסוג הזה הוא לשרת את המשתמש הבודד. לכן מערכת הפעלה כזו משותתת על עקורונות של נוחות למשתמש וזמן תגובה מהיר. בשנים האחרונות התעצמה המגמה של ריבוי מעבדים במחשבים ביתיים, ולכן הגבול בין מערכות הפעלה מקביליות למערכות הפעלה למחשבים ביתיים הולך ומיטשטש.
  * **מערכות הפעלה זמן אמת (real-time operating system) &#8211;** במערכת זמן אמת הדגש הוא על זמן הביצועים. ניתן להבחין בין 2 סוגי מערכות זמן אמת: מערכות שמציבות אילוצים נוקשים על זמני ביצוע (hard real time) ומערכות שהאילוצים גמישים יותר (soft real time). למערכות מהסוג הראשון ניתן לשייך מערכות במטוסים ומכוניות. ולסוג השני אפשר לשייך, לדוג', מערכות מוטלימדיה (בהן אי עמידה בזמנים יכול להיות נסבל במידה מסוימת).
  * **מערכות הפעלה למערכות משובצות ([embedded operating system](https://en.wikipedia.org/wiki/Embedded_operating_system)) &#8211;** מערכות הפעלה אלו מיועדות לשימוש בסמארטפונים, ב smartcards וכד'. מערכות משובצות מתאפיינות בהצבת דרישות מחמירות מאוד על שימוש במשאבי המערכת.

&nbsp;

### 4. מושגים בסיסיים

<img src="/images/posts/operating-system-part-1/ubuntu_terminal.jpg" alt="Ubuntu Terminal">

במהלך הפוסטים הבאים נעמיק יותר בנושאים הבאים, אך כדי כבר להכירם היכרות ראשונית ולהבין באופן כללי את משמעותם נעבור עליהם באופן מהיר:

* **תהליך (process) &#8211;** תכנית ריצה (executable) בביצוע. באופן בסיסי, תהליך מכיל את התכנית עצמה (code), את התונים שהיא יוצרת ומשתמשת בהם (data), מצביע למחסנית, מונה פקודות, ואוגרים אחרים שמכילים מידע על הסטטוס הנוכחי של הביצוע (התהליך גם מכיל מידע על הקבצים שהוא משתמש בהם, ונתונים רבים נוספים, אך על זה נרחיב בהמשך).
* **מצב קיפאון (deadlock) &#8211;** קבוצה של תהליכים נמצאת במצב קיפאון אם כל אחד מהתהליכים אינו יכול להתקדם אלא לאחר שיקרה אירוע אשר יכול להיגרם אך ורק על ידי תהליך אחר בקבוצה. תופעת הקיפאון בצורתה הפשוטה ביותר מתרחשת כאשר קיימים מינימום של שני תהליכים, שכל אחד מחזיק ברשותו משאב בלעדי הנחוץ לתהליך השני. במצב זה אף אחד מהתהליכים אינו יכול להתקדם.
* **ניהול זיכרון (memory management) &#8211;** בהמשך נדבר על שיטות ניהול זיכרון המאפשרות לשכן בו זמנית מספר תהליכים בזיכרון, ואף בחלק מהמקרים להריץ תוכניות שמשתמשות בכמות של זיכרון גדולה יותר מהזיכרון הפיזי.
* **קלט / פלט (input / output) &#8211;** התקן קלט / פלט הוא רכיב חומרה אשר נועד לאחסן ו/או להעברת מידע. לדוג' דיסק קשיח, דיסק און קיי, כרטיס רשת וכ'ו. ישנם התקני קלט / פלט אשר משמשים כהתקני קלט בלבד (לדוג' עכבר ומקלדת), או כהתקני פלט בלבד (לדוג' מדפסת ומסך). אחד התפקידים החשובים ביותר של מערכת ההפעלה הוא הניהול של התקנים אלו.
* **קבצים (files) &#8211;** קובץ הוא יחידת מידע לוגית לאחסון במדיה חיצונית. כיוון שקבצים הם מבנים לוגיים, מימושים נעשה בתוכנה ולא בחומרה. מערכת ניהול הקבצים (שהיא חלק ממערכת ההפעלה) אחראית למימוש הקבצים.
* **מעבד פקודות סדרתי (shell) &#8211;** תכנית המהווה ממשק אינטראקטיבי למערכת ההפעלה. ה shell מקבל פקודות שמוקלדות ע"י המשתמש ומבצע אותן על ידי שימוש בשירותי מערכת ההפעלה.

&nbsp;

### 5. קריאות מערכת

מערכת ההפעלה לא רק מנהלת את החומרה, אלא גם צריכה להגן על משאבי המערכת (לדוג', מפני הרצה של קוד זדוני במעבד). הגנה כזאת איננה יכולה להיות תוכנתית, מכיוון שאם מערכת ההפעלה תקבל כל פקודה ופקודה ותצטרך לנתח אותה (ואולי גם בהתאם לפקודות הקודמות שקיבלה מאותה תוכנית) לפני העברתה למעבד הדבר ישפיע בצורה קריטית על משאבי המערכת (בהנחה וזה בכלל אפשרי, הרי שורת קוד אחת לבדה יכולה להיות תמימה, אך בצירוף כמה שורות נוספות יהיה מדובר כבר על קוד זדוני שיכול להסב למערכת נזק).

לכן, המסקנה היא שההגנה צריכה להיות חומרתית, ז"א ביט דלוק (1) או מכובה (0) שמייצג מצב מיוחס (kernel mode) או מצב משתמש (user mode). כאשר תוכנה מסויימת מבקשת את השירותים של המעבד, כדי לבצע חישוב כלשהו, המערכת תעביר את הביט במעבד למצב user mode ותעביר את השליטה לאותה תוכנה כדי לבצע את חישוביה. מכאן ישנן 2 אפשרויות:

* הראשון הוא שהתוכנה תסיים את פעולותיה ותחזיר את המעבד למערכת ההפעלה, אך נזכור שכרגע המעבד במצב user mode ואי אפשר לבצע איתו פעולות מסויימות, כמו לדוג' להדליק את הביט ולהעביר את המעבד למצב kernel mode. אז נשארנו נעולים ב user mode, עד מתי? עד איזה time out? (אז מי מבטיח שהתוכנה תחזיר את משאבי המעבד למערכת ההפעלה לפני ה time out ולא תשאיר אותו אצלה גם אחרי שיקרה ה time out והמעבד יחזור למצב kernel mode?).
* האפשרות השניה היא שהתוכנה תשאיר אצלה את המעבד עד אין סוף, ולא תחזיר את המשאבים למערכת ההפעלה, ובקיצור תתקע את המחשב. 

מה שמכריח את התוכנה להחזיר את משאבי המעבד חזרה למערכת ההפעלה הוא system call. ישנן מספר פעולות שאינן יכולות להתבצע ב user mode, אלא אך ורק ב kernel mode. כשהתוכנה רוצה לבצע את אחת מהפעולות הללו (לדוג', להתחיל תהליך חדש, או לקרוא ולכתוב אל מערכת הקבצים) היא מבצעת system call כדי לבקש ממערכת ההפעלה לעשות זאת בשבילה. בעת ביצוע ה system call מורמת פסיקה (Interrupt) שנתפסת ע"י בקר הפסיקות (PIC &#8211; ראשי תיבות של Programmable Interrupt Controller. בקר הפסיקות הינו רכיב פיזי, לדוג' [Intel 8259](https://en.wikipedia.org/wiki/Intel_8259)), והוא זה שמעביר את השליטה למערכת ההפעלה ומדליק את הביט במעבד כדי להעבירו למצב מיוחס (kernel mode).

הבקר פסיקות, מרים בנוסף פסיקות כל זמן מסוים, רק כדי לוודא שגם האפשרות השניה (בה התוכנה אינה תשחרר את משאבי המעבד לעולם) לא תקרה. גם כאשר מדובר על פסיקות המורמות כל זמן מסוים (time out) (וגם כאשר מורמות פסיקות כתוצאה מ system call) הפסיקה מתקבלת אצל המעבד בהפתעה גמורה, הוא אינו מודע לכך שהיא אמורה לקרות.

בתחילת הפוסט ראינו כי ביצוע של הוראות מיוחסות מתאפשר רק במצב מיוחס (kernel mode), ולמשתמש רגיל לא ניתנת אפשרות כזאת. אך, כמו שאמרנו, לרשות המשתמש עומד ממשק מיוחד של קריאות מערכת (system call) שדרכו הוא יכול לבקש ממערכת הפעלה שירותים אשר דורשים הרשאות מיוחדות. השירותים שמערכת ההפעלה מספקת יכולים להתבקש ע"י תכנית הכתובה בשפה עילית בצורה של פונקציות. כל קריאת מערכת מוציאה את השליטה מידי תכנית המשתמש ומעבירה אותה באופן זמני למערכת ההפעלה (מי שמבצע זאת בפועל זה בקר הפסיקות). התוצאה של הפעולה איננה ודאית, ולכן עבור כל קריאת מערכת, מערכת ההפעלה מחזירה אינדיקציה על תוצאת הביצוע (וחייבת להתבצע בדיקה של הערך שהפונ' מחזירה). 

כדי להבין כיצד עוברת השליטה למערכת ההפעלה בעת הקריאה פונקציות אשר מכילות קריאת מערכת, להלן תוכנית בשפת C המדפיסה "hello world" על המסך, ומשתמשת בפונ' write אשר מכילה קריאה לשירות של מערכת ההפעלה.

```c
#include &lt;unistd.h&gt;
#include &lt;string.h&gt;
#define STDOUT 1

int main(){
    char *msg[] = "Hello wold\n\0";
    if (write(STDOUT, msg, strlen(msg)) &lt; 0)
        exit(1);
    return(0);
}
```

להלן התוכנית בשפת assembly שמבצעת את המשימה:

```c
.data			# Data section

msg:	.asciz "Hello world\n"	# The string to print
	len = . - msg - 1	# The length of the string

.text			# Code section
.global	_start

_start:			# Entry point
	push1	$len		# Arg 3 to write: length of string
	push1	$msg		# Arg 2: pointer to string
	push1	$1		# Arg 1: file descriptor
mov1	$4, %eax	# Write
	call	do_syscall
	add1	$12, %esp	# Clean stack

	push1	$0		# Exit status
mov1	$1, %eax	# Exit
	call	do_syscall

do_syscall:
	int	$0x80		# Call kernel
	ret
```

בשורות 10-12 מתבצעת העברת שלושה פרמטרים המכילים אינדיקציה של יעד הפלט (STDOUT), מצביע להודעה הנפלטת, ומספר התווים שבהודעת. בשורה 13 מועבר מספר השירות המסופק על ידי מערכת ההפעלה (במקרה שלנו write). ובשורה 22 מתבצעת הוראת TRAP שמעבירה את המעבד למצב מיוחס וגורמת למעבר השליטה למערכת ההפעלה.

מערכת ההפעלה, תבדוק את הפרמטרים שהועברו בשורות 10-13, ואם הכל נמצא תקין היא תספק למשתמש את השירות המבוקש (במקרה שלנו תבצע הדפסה של הודעה על למסך).

להלן הרשימה של הקריאות מערכת (system calls) במערכות UNIX:

| UNIX | WIN32	| Description |
| :---------:|:-----:|:----:|
| fork | CreateProcess	| Create a new process	|
| waitpid | WaitForSingleObject | Can wait for a process to exit |
| execve | (none) | CreateProcess = fork + execve |
| exit | ExitProcess | Terminate execution |
| open | CreateFile | Create a file or open an existing file |
| close | CloseHandle | Close a file |
| read | ReadFile | Read data from a file	|
| write | WriteFile | Write data to a file |
| lseek | SetFilePointer | Move the file pointer |
| stat | GetFileAtterbutesEx | Get various file attributes |
| mkdir | CreateDirectory | Create a new directory |
| rmdir | RemoveDirectory | Remove an empty directory |
| link | (none) | Win32 does not support links |
| unlink | DeleteFile | Destroy an existing file |
| mount | (none) | Win32 does not support mount |
| umount | (none) | Win32 does not support mount |
| chdir | SetCurrentDirectory | Change the current working directory |
| chmod | (none) | Win32 does not support securiry (although NT does)	|
| kill | (none) | Win32 does not support signals |
| time | GetLocalTime | Get the current time |

<img src="/images/posts/operating-system-part-1/monolithic_systems.png" alt="Monolithic Systems" style="width: 50%;">

&nbsp;

### 6. המבנה של מערכות הפעלה

מערכות הפעלה הן מערכות גדולות, המכילות, לרוב, עשרות ולפעמים מאות אלפי שורות קוד. אך כדי שכל האופרציה הזאת תפעל כשורה דרוש עיצוב כללי כלשהו, ולכל מערכת יש רעיון עיצובי משלה:

* מערכות מונוליתיות (monolithic systems) - מערכת מונוליתית היא למעשה אוסף גדול של פונקציות שונות.
* מערכות מרובדות (layered systems) - אלו הן מערכות שמרכיביהן מאורגנים ברבדים הנמצאים ביחס היררכי. לכל רובד מוגדר ממשק שדרכו הרבדים הסמוכים בהיררכיה יכולים לתקשר בינהם.

| Function | Layer|
|:----:|:--------:|
| The operator | 5 |
| User programs | 4 |
| input/output management | 3 |
| Operator-process communication | 2 |
| Memory and drum management | 1 |
| Processor allocation and multiprogramming | 0 |

* מכונה מדומה (virtual machine) &#8211; בחלק הראשון ראינו שאחד התפקידים של מערכת ההפעלה הוא אספקה של שירותים של המכונה המורחבת ושל המכונה המדומה. ניתן לראות את מערכת ההפעלה כשכבת תוכנה המספקת לשכבות שמעליה מס' העתקים של החומרה עם כמות משאבים פחותה מזו שבחומרה הפיזית בפועל (במובן מסוים זו אינה מערכת הפעלה רגילה, שכן על כל מכונה מדומה יכולה לרוץ מערכת הפעלה חדשה). התוכונות הפופלריות בשוק כדי ליצור ולהפעיל מכונות מדומות הן [virtualbox](https://www.virtualbox.org/wiki/Downloads) של חברת oracle ו [vmware](http://www.vmware.com/il).
* מערכות Exokernel &#8211; במערכות אלה השירותים המסורתיים כגון מערכת קבצים, ניהול זיכרון, תזמון תהליכים ותקשורת הוצאו אל מחוץ לגרעין של מערכת ההפעלה. ההחלטה הזאת נובעת מכך שמערכת ההפעלה איננה כופה על המשתמש את צורת השימוש במשאבים (אלא רק דואגת להגנה על המשאבים וניהולם).
* מערכות שרת לקוח (client &#8211; server systems) &#8211; מערכות שרת לקוח מבוססות על הרעיון של גרעין מנינימליסטי (micro kernel), ז"א גרעיון מערכת ההפעלה מתפקד כדוור המריץ בקשות של לקוחות (תהליכים) אל שרתים עצמאיים (גם תהליכים), המפוזרים במערכת, כגון שרתי מערכת הקבצים, מנהל הזיכרון, תכנית התקשורת, תכנית המסך (מנהל חלונות), וכ'ו. כאשר מתקבלות תשובות מהשרתים, הגרעין מחזיר את התשובה להתליך המבקש. בשיטה זו התוכנה מורכבת מיחידות עצמאיות, שכל אחת מהן ממלאת תפקיד מוגדר. שיטה זו מצמצת מאוד את התלות בחומרה.

&nbsp;

### סיכום

בחלק זה למדנו את שני התפקידים של מערכת ההפעלה, ראינו מהן קריאות מערכת, ביצענו יישור קו לגבי הסוגים השונים של המבנה של מערכות הפעלה, ועברנו גם על מושגים יסודיים בתחום (קבצים, תהליכים, ניהול זיכרון, וכד'). חלק זה הינו תיאורטי (ברובו) ואנו עדין לא צוללים אל עומק הדברים, למרות זאת הבסיס הוא חשוב להבנה לפני שממשיכים לפן הטכני של הנושא (כדי שלא נאבד את הידיים והרגליים).
