---
isChild: true
title:   MySQL Extension
anchor:  mysql_extension
---

## תוסף MySQL {#mysql_extension_title}

תוסף ה-[mysql] ל-PHP אינו נמצא בפיתוח פעיל [ולא מומלץ לשימוש באופן רשמי (deprecated) החל מגרסה PHP 5.5.0]
כאשר אנו מציינים [mysql_deprecated], אנו מתכוונים לכך שהתוסף יוסר בטווח של כמה גרסאות. אם אתם מבצעים שימוש באחר
מהפונקציות המתחילות ב-`mysql_*` כגון: `mysql_connect()` ו- `mysql_query()` באפליקצייה שלכםת קחו בחשבון שהן פשוט 
לא יהיו זמינות בגרסאות הבאות של PHP. המשמעות היא שאתם צפויים לבצע שכתובי קוד והאפשרות הטובה ביותר
היא להחליף את השימוש ב-mysql עם [mysqli] או [PDO] באפליקצייה שלכם בתכנון מראש של שלבי הפיתוחת כך שלא תופתעו לאחר מכן. 

**אם אתם מתחילים פרויקט חדשת בשום פנים אל תשתמשו בתוסף ה-[mysql]: השתמשו ב-[MySQLi extension][mysqli],
או ב-[PDO].**

* [PHP: בחירת API עבור MySql][mysql_api]
* [מדריך PDO עבור מפתחי MySQL][pdo4mysql_devs]


[mysql]: http://php.net/mysql
[mysql_deprecated]: http://php.net/migration55.deprecated
[mysqli]: http://php.net/mysqli
[pdo]: http://php.net/pdo
[mysql_api]: http://php.net/mysqlinfo.api.choosing
[pdo4mysql_devs]: http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers
