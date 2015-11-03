---
isChild: true
anchor:  command_line_interface
---

## ממשק שורת הפקודה {#command_line_interface_title}

שפת ה-PHP נוצרה כדי לכתוב אפליקציות רשת, אך היא שימושית עבור תכניות סקריפט לממשקי שורת פקודה (CLI)
תכניות PHP לשורת הפקודה יכולות לסייע במיכון מטלות שכיחות כגון בדיקות, פריסה וניהול אפליקציות.

תכניות CLI PHP הן כלי שימושי ועוצמתי המאפשר שימוש ישיר בקוד האפליקציה שלנו בלי הצורך ליצור ולאבטח ממשק גרפי למשתמש
(GUI). רק וודאו **שלא** לשים את קבצי סקריפט ה-CLI שלכם בתיקיה הציבורית שבשרת!

נסו להריץ PHP משורת הפקודה:

{% highlight console %}
> php -i
{% endhighlight %}

האפשרות `-i` תדפיס למסך מידע על קונפיגורציית ה-PHP המותקנת, בדיוק כמו הפקודה [`phpinfo()`][phpinfo].

האפשרות `-a` מאפשרת עבודה עם מעטפת PHP אינטראקטיבית, בדומה ל-IRB של רובי (ROR) או המעטפת של פייטון (Python).
קיימות מספר [אפשרויות שימושיות נוספות][cli-options] לעבודה עם ממשק שורת הפקודה.

הבה ונכתוב תכנית CLI פשוטה, "Hello, $name". כדי לנסות ולהריץ אותה, צרו קובץ הנקרא `hello.php`, כמפורט להלן.

{% highlight php %}
<?php
if ($argc !== 2) {
    echo "Usage: php hello.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hello, $name\n";
{% endhighlight %}

בשפת ה-PHP הוגדרו שני משתנים מיוחדים המבוססים על הארגומנטים אשר הסקריפט מורץ איתן. [`$argc`][argc] הוא משתנה 
אינטגר (Integer) המכיל את הארגומנט *count* ו- [`$argv`][argv] הוא מערך המכיל את ערכי *value* המשתנים שנשלחו עם הסקריפט.   
המשתנה הראשון במערך זה הוא תמיד שם קובץ הסקריפט, במקרה זה -  `hello.php`.

הביטוי `exit()` נמצא בשימוש עם ערך השונה מאפס כדי ליידע את המעטפת שהפקודה נכשלה. ערכי קוד מקובלים לפקודה זו
ניתן למצוא [כאן][exit-codes].


נסו להריץ PHP משורת הפקודה:

{% highlight console %}
> php hello.php
Usage: php hello.php [name]
> php hello.php world
Hello, world
{% endhighlight %}


 * [למדו על הרצת PHP משורת הפקודה][php-cli]
 * [למדו על הגדרות הרצת PHP משורת הפקודה על windows][php-cli-windows]


[phpinfo]: http://php.net/function.phpinfo
[cli-options]: http://php.net/features.commandline.options
[argc]: http://php.net/reserved.variables.argc
[argv]: http://php.net/reserved.variables.argv
[exit-codes]: http://www.gsp.com/cgi-bin/man.cgi?section=3&amp;topic=sysexits
[php-cli]: http://php.net/features.commandline
[php-cli-windows]: http://php.net/install.windows.commandline
