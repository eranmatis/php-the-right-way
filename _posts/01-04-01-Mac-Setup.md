---
isChild: true
anchor:  mac_setup
---

## התקנת Mac {#mac_setup_title}

מערכות ההפעלה OS X מכילות בתוכן PHPת אך בדרך כלל לא עם הגרסה המעודכנת ביותר. גרסת Mountain Lion מכילה PHP 5.3.10,
גרסת Mavericks מכילה PHP 5.4.17 וגרסת Yosemite מכילה PHP 5.5.9, אבל לעיתים גרסאות אלו אינן מספיקות לעומת PHP 5.6.

קיימות דרכים רבות להתקין PHP על OS X.

### התקנת PHP באמצעות Homebrew

[Homebrew] הוא מנהל התקנים חזק בשימוש מערכת ההפעלה OS X, באמצעותו ניתן להתקין PHP ותוספים נוספים בקלות.
[Homebrew PHP] הוא מאגר המכיל "מתכונים" הקשורים ל-PHP עבור Homebrew ויאפשר גם התקנת PHP.

נכון לעכשיו, ניתן להתקין `php53`, `php54`, `php55` או `php56` באמצעות פקודת `brew install` ולהחליף ביניהם 
באמצעות עדכון של משתנה ה-`PATH` שבתחנת העבודה שלך.
לחילופין, ניתן להשתמש ב- [brew-php-switcher][brew-php-switcher] שיבצע את ההחלפה באופן אוטומטי עבורך..

### התקנת PHP באמצעות Macports

פרויקט ה-[MacPorts] הוא יוזמה של קהילת קוד מקור פתוח לעצב מערכת פשוטה להידור (קומפילצייה), התקנה ושדרוג
באמצעות ממשק שורת הפקודה, X11 או תכנת קוד מקור פתוח מבוססת Aqua על גבי מערכת ההפעלה OS X.

MacPorts תומכת בקבצים בינאריים מהודרים כך שאין צורך להדר מחדש כל תלות
מקבצי מקור דחוסים, וממש מצילת חיים במקרים בהם לא מותקנת אף חבילה במערכת שלך.

נכון לעכשיו, ניתן להתקין `php53`, `php54`, `php55` או `php56` באמצעות פקודת `port install`, לדוגמא:

    sudo port install php54
    sudo port install php55

ניתן להריץ את פקודת ה- `select` על מנת להחליף בין סביבת ה-PHP הפעילה:

    sudo port select --set php php55

### התקנת PHP באמצעות phpbrew

[phpbrew] כלי להתקנת וניהול גרסאות מרובות של PHP. כלי זה שימושי מאוד במצבים בהם שתי מערכות או מוצרים דורשות
גרסאות שונות של PHP ובמידה שלא נעשה שימוש במכונות וירטואליות.

### התקנת PHP באמצעות התקנה בינארית של Liip
אפשרות נפוצה נוספת היא [php-osx.liip.ch] המספקת דרכי התקנה רציפות עבור גרסאות PHP 5.3 ועד 5.6.
ההתקנה מתבצעת במיקום נפרד (/usr/local/php5), כך שאין שכתוב של קבצי ה-PHP המוקתנים ע"י Apple.

### הידור מהמקור

שיטה נוספת המעניקה שליטה על גרסת ה-PHP המותקנת היא שעטת [הדר זאת בעצמך][mac-compile].
אם נעשה שימוש בשיטה זו, יש לוודא שכבר התקנו [Xcode][xcode-gcc-substitution] או תחליף אחר של חברת Apple
["כלים לשורת הפקודה עבור XCode"] הניתנים להורדה מאתר מרכז הפיתוח של Apple's Mac.

### התקנות משולבות (הכל כלול)

הפתרונות הקודמים מטפלים בעיקר ב-PHP עצמו אך אינם מספקים כלים כמו Apache, Nginx או SQL server.
פתרונות "הכל כלול" כגון: [MAMP][mamp-downloads] ו/או [XAMPP][xampp] יתקינו את הכלים הנוספים הנדרשים גם כן
ויגדירו את הקשרים ביניהם באופן אוטומטי. אך לפשטות ההתקנה יש מחיר של גמישות היישום.

[Homebrew]: http://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[php-osx.liip.ch]: http://php-osx.liip.ch/
[mac-compile]: http://php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[mamp-downloads]: http://www.mamp.info/en/downloads/
[xampp]: http://www.apachefriends.org/en/xampp.html
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher
