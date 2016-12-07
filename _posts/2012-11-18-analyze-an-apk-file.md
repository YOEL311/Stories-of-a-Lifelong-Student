---
title: Analyze an Apk file
author: nirgn
layout: post
summary: "כמו שזכור לנו, אנדרואיד בנויה כולה מקבצי Apk ולכן בפוסט הזה נלמד כיצד לפתוח אותם, לבצע בהם שינויים, ולבסוף לבנות ולחתום אותם מחדש. בפוסט אדגים על קובץ Apk של אפליקציה מה Play, אך כמובן שאתם יכולים לעשות את זה עם כל אפליקציה."
category: Android
---
אחד הדברים השימושיים (והמגניבים) באנדרואיד הוא לדעת לפתוח ולחתום קבצי Apk וכמובן כתוצאה מכך היכולת לערוך אותם.

כמו שזכור לנו, אנדרואיד בנויה כולה מקבצי Apk ולכן בפוסט הזה נלמד כיצד לפתוח אותם, לבצע בהם שינויים, ולבסוף לבנות ולחתום אותם מחדש. בפוסט אדגים על קובץ Apk של אפליקציה מה Play, אך כמובן שאתם יכולים לעשות את זה עם כל אפליקציה (כולל אלו המגיעות בצורה מובנת במערכת).

קודם כל על מנת לדעת מהו קובץ Apk ועל איך הוא בנוי קראו את הפוסט [A little bit of Android Grammar](http://www.lifelongstudent.net/2012/03/little-android-bit-grammar/). בנוסף אתם צריכים להתקין JDK ו JRE [מפה](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

<!--more-->

&nbsp;

### הכנות

בשביל לפתוח את קבצי ה Apk ואחר כך לבנות אותם מחדש, ניעזר בתוכנה ApkTool (הורידו את הקובץ [apktool1.5.2.tar.bz2](https://android-apktool.googlecode.com/files/apktool1.5.2.tar.bz2)).

ובנוסף, את הקובץ [apktool-install-windows-r05-ibot.tar.bz2](https://android-apktool.googlecode.com/files/apktool-install-windows-r05-ibot.tar.bz2) (אם אתם משתמשים ב Windows), או את הקובץ [apktool-install-linux-r05-ibot.tar.bz2](https://android-apktool.googlecode.com/files/apktool-install-linux-r05-ibot.tar.bz2) (אם אתם משתמשים ב Linux).

לאחר מכן, חלצו את הקובץ Jar שנמצא בתיקייה הנמצאת בתוך הקובץ הראשון שהורדנו (apktool1.5.2.tar.bz2) לתיקייה שהגיעה מתוך הקובץ השני (של ה Windows או ה Linux). יש לציין כי אתם יכולים למקם את התיקייה הנל איפה שנוח לכם, אני ממליץ על הנתיב `usr/local/bin/` ב Linux, או ב Windows בנתיב `C:\Program Files\Android\android-sdk\platform-tools`.

&nbsp;

### Decompile

  1. העבירו את האפליקציה (קובץ ה Apk), לתיקייה apktool.
  2. פתחו את ה ה Terminal (או את ה Cmd), נווטו למיקום בו מיקמתם את התיקייה, apktool.
  3. כדי לפתוח / לשבור את הקובץ נכתוב `apktool d namOfTheApp.apk nameOfTheFolder`.
      * את ה namOfTheApp החליפו בשם הקובץ, ואת ה nameOfTheFolder החליפו בשם שבו אתם רוצים לקבל את התיקייה (היא תיווצר בתוך התיקייה apktool).
      * ב Linux הוסיפו /. לפני הפקודה.
      * האות d שנמצאת לאחר ה apktool בפקודה, הינה קיצור של decompile.

דוגמה (ב Linux): אם שם הקובץ אותו נרצה לשבור הוא HelloWorld.apk, נכתוב: `apktool d HelloWorld.apk appOne/.` , תיווצר לנו תיקייה בשם appOne (בתוך התיקייה apktool).

&nbsp;

### Build

כדי לבנות את האפליקציה מחדש אנו נדרשים (בשלב האחרון) לחתום אותה. כל אפליקציה נדרשת להיות חתומה בצורה דיגיטלית, המפתח של החתימה הינו פרטי ונמצא בידי מפתח האפליקציה.

החתימה, או במילים אחרות התעודה הדיגיטלית, מספקת למערכת האנדרואיד אמצעי לזהוי המפתח של האפליקציה, ולביסוס קשר אמין בין אפליקציות.

הנקודות החשובות שצריך להבין לגבי חתימות הן:

  * כל האפליקציות נדרשות להיות חתומות. המערכת לא תתקין אפליציות לא חתומות על המכשיר, או על האמולטור.
  * כדי לבחון ולדבג את האפליקציות שהמפתחים בונים, ה Android SDK חותם אותם באופן אוטומטי על ידי מפתח גנרי שהוא מחולל, המיוחד בשביל לביצוע Debug.
  * כשהמפתח משחרר את הגרסה ל Play היא חייבת להיות חתומה על ידי מפתח פרטי, לא ניתן לשחרר את האפליקציה כשהיא חתומה על ידי המפתח שה Android SDK מחולל.
  * לכל תעודה יש תאריך תפוגה, כשעבר תאריך זה המערכת לא תתקין אפליקציות החתומות על ידי תעודה זו. אך יש לציין כי המערכת בודקת את התאריך הנל רק בעת התקנת האפליקציה, ואם התאריך עבר לאחר שהאפליקציה הותקנה, האפליקציה תמשיך לתפקד כרגיל.
  * ניתן להשתמש בכלים רגילים (כמו Keytool ו Jarsigner) כדי לחולל (לייצר) מפתח בשביל לחתום את האפליקציה.

&nbsp;

**נתחיל בבניה:**

1. בשביל לבנות את האפליקציה, נכתוב את הפקודה הבאה `apktool b nameOfTheFolder nameOfTheApp.apk`.
    * את הפקודה יש לכתוב, כמובן, בטרמינל (או ב Cmd) ולהיות בנתיב של התיקייה apktool.
    * את nameOfTheFolder החליפו כמובן בשם התיקייה בה נמצאים הקבצים, ואת nameOfTheApp החליפו בשם שתרצו לקרוא לאפליקציה.
    * ב Linux הוסיפו /. לפני הפקודה.
    * האות b שנמצאת לאחר ה apktool בפקודה, הינה קיצור של build (או recompile).
2. בשביל לייצר מפתח איתו נוכל לחתום את הקובץ apk, יש להתקין את ה Android SDK. לאחר מכן נפתח את הטרמינל (או Cmd) ונכתוב `keytool -v -genkey -v -keystore nameOfKey.keystore -alias aliasName -keyalg RSA -validity 10000`.
    * genkey הינו קיצור של generate key.
    * v הינו קיצור של verbose mode (מצב מפורט).
    * nameOfKey, יהיה שם המפתח (ניתן להחליף לכל מה שבא לכם).
    * aliasName יוצר כינוי (שם אחר) למפתח (ניתן להחליף לכל מה שבא לכם).
    * keyalg מפרט את האלגוריתם הצפנה המשמש לחולל את המפתח (קרי [RSA](http://en.wikipedia.org/wiki/RSA_(cryptosystem)), [DSA](http://en.wikipedia.org/wiki/Digital_Signature_Algorithm) וכד').
    * validity מתאר בימים לכמה זמן המפתח תקף (במקרה זה כתבתי 10,000 ימים).
    * כחלק מהיצירה של המפתח תצטרכו למלא פרטים אישיים, ולבחור סיסמה למפתח.
3. כעת נחתום את האפליקציה, ובשביל קיצור הפקודה, העבירו את הקובץ apk ואת המפתח לאותה תיקייה, וכתבו בטרמינל (או ב Cmd) את הפקודה `jarsigner -verbose -keystore myKeyName.keystore appName.apk aliasName`.
    * myKeyname זהו שם המפתח שיצרנו בסעיף לעיל.
    * appName זהו שם הקובץ apk.
    * aliasName זה הכינוי של המפתח שכתבו בסעיף לעיל.
    * יש לציין כי בעת החתימה תצטרכו להכניס את הסיסמה של המפתח.

&nbsp;

### Framework

בתכנות מונחה עצמים ישנה ספרייה המחברת את כל חלקי המערכת למערכת אחת, הספרייה הזאת מכונה Framework (או בעברית, שלד).

מערכת ה Android כתובה ב Java שהינה שפה מונחת עצמים, לכן גם ל Android יש Framework. ה Framework של Android AOSP מגיע מובנה בספרייה של apktool, אך כחלק מהשינויים שהיצרניות השונות מבצעות במערכת, הן מבצעות שינוים גם ב Framework, לכן אם נרצה לפתוח קבצי Apk של סמסונג או HTC וכד', נצטרך לעדכן את קבצי ה Framework שלהם.

בשביל לעדכן, יש לחלץ את הקובץ framework-res.apk (מהספרייה `system/framework/`).

  * במכשירים של סמסונג, נצטרך את הקובץ framework-res.apk ואת הקובץ twframework-res.apk.
  * במכשירים של HTC, נצטרך את הקובץ com.htc.resources.apk בלבד.

את הקבצים נמקם בתקייה apktool, וכדי להתקינם נכתוב ב Cmd (או בטרמינל) `apktool if framework-res.apk`.

  * במידה והפקודה נכתבת בלינוקס יש להוסיף /. לפני ה apktool.
  * if זהו קיצור של install framework.

במידה וה Framework הותקן בהצלחה, נקבל את התוצאה: `I: Framework installed to yourPath 1.apk`.

<div class="left">
  <img src="/images/posts/analyze-an-apk-file/Notepad.png" alt="Notepad" style="width: 35rem;">
</div>

&nbsp;

### Look Inside

כעת, כשפתחנו את קובץ ה Apk אנו יכולים לבצע מגוון שינויים. לדוגמה, בתיקיית ה res נמצאים המשאבים של האפליקציה, כמו תמונות, קבצי xml וכד'.

בדוגמה מצד שמאל, פתחתי את האפליקציה של Youtube ונכנסתי לתיקייה res ומשם לתקייה values ופתחתי את הקובץ settings עם תוכנת ה[Notepad++](http://notepad-plus-plus.org/)(מי שמשתמש בהפצת לינוקס כלשהי, אני ממליץ על העורך [Sublime Text 2](http://www.sublimetext.com/2)), ותרגמתי כמה מהלחצנים (שימו לב שאתם מתרגמים את מה שבשחור, בין ה <> , ניתן לראות את הסימן בתמונה.

בנוסף, אפליקציות מורכבות מתמונות, אם זה רקע, לחצנים וכד'. ניתן לערוך אותם בעזרת ה Photoshop (או Gimp), בדוגמה מצד ימין פתחתי את האפליקציה של Shazam וצבעתי את הרקע המוכר של האפליקציה (שהינה תמונה) באדום (למה? כי אני יכול (; ).

<div class="left">
  <img src="/images/posts/analyze-an-apk-file/Red_Background_Shazam.png" alt="GSM Architecture" style="width: 15rem;">
</div>

והרי כמו שאמרנו, המערכת מורכבת מקבצי Apk, לכן, ניתן לתרגם כך את כל המערכת (אפליקציית החייגן, הודעות, אנשי קשר, הגדרות וכד'), אם תפתחו (בעזרת Winrar או 7Zip) את ה Rom שהורדתם (שבעצם הינו קובץ zip) תשימו לב שישנה תיקייה בשם system, ובתוכה תיקייה בשם app ובה נמצאים כל קבצי ה Apk שדיברנו עליהם.

  * בנוסף, בתיקיית ה fonts נמצאים הפונטים (החל מגרסת Android 2.2 קיימים פונטים בעברית, אך ניתן להחליף אותם לפונט אחר במידה ותרצו).
  * בתיקיית ה media נמצאים ההתראות, רינגטונים, וקבצי מערכת (כמו הקליק של המצלמה וכד').
  * בפוסט [ליצור Boot Animation ב 5 שלבים](http://www.lifelongstudent.net/2012/04/%d7%9c%d7%99%d7%a6%d7%95%d7%a8-boot-animation-%d7%91-5-%d7%a9%d7%9c%d7%91%d7%99%d7%9d/) ישנו הסבר מעמיק, כיצד לבנות ולהחליף את אנימציית ההפעלה של המכשיר (bootAnimation).
  * בתיקייה framework נמצא הקובץ framework.res.apk שאחראי על התרגום של שאר המערכת (במקומות שלא שייכים לקבצי Apk ספצייפים כמו החייגן), לדוגמה: תפריט הכיבוי, כפתורי אישור, מסך נעילה וכד'.

&nbsp;

### סיכום

אני מקווה שהמדריך היה מובן והצלחתם לבצע את שרציתם ללא שגיאות. אני מאוד ממליץ לשתף את התוצאות בפורומים השונים (תוכלו לחסוך זמן למי שרוצה לבצע את אותו השינוי). במידה ויש שאלות או שנתקלתם בשגיאה כלשהי אשמח לנסות לעזור בתגובות.