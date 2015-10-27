---
isChild: true
title:   Abstraction Layers
anchor:  databases_abstraction_layers
---

## שכבות הפשטה {#databases_abstraction_layers_title}

מערכות רבות מממשות בעצמן שכבות הפשטה באופן התואם או שלא תואם ל-[PDO][1]. הן בדרך כלל יחקו
תכונות עבור מערכת לאחרון נתונים אחת אשר תכונותיה חסרות ממערכת אחרת ע"י עטיפה של השאילתות במתודות PHP,
וכך לספק הפשטת נתונים במקום רק הפשטת חיבור אשר מספק ה-PDO. כמובן שתהיה תקורה מסויימת, אבל אם אנו בונים אפליקציית פורטל
אשר נדרשת לעבוד עם MySQL, PostgreSQL and SQLite אז במקרה זה, תקורה מסויימת קבילה על חשבון ניקיון הקוד.

שכבות הפשטה מסויימות נבנו תוך שימוש בתקינת שמות מרחב (namespace) [PSR-0][psr0] או [PSR-4][psr4] ולכן ניתן להשתמש בהן
 בכל אפליקציה שנרצה.
* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [ZF2 Db][4]


[1]: http://php.net/book.pdo
[2]: http://www.doctrine-project.org/projects/dbal.html
[4]: http://packages.zendframework.com/docs/latest/manual/en/index.html#zend-db
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
