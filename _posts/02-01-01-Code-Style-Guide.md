---
anchor: code_style_guide
---

# הנחיות וכללים לקידוד {#code_style_guide_title}

קהילת ה-PHP גדולה ומגוונת, מורכבת מאינספור ספריות קוד, מערכות מסגרת ורכיבים. מפתחי PHP נוהגים לבחור את 
הרכיבים המתאימים להם ולגבשם לפרויקט בודד. מכאן נובעת החשיבות הגדולה לשמירה על כללי קידוד ברורים
(עד כמה שניתן) ומשותפים כדי לאפשר למפתחים אחרים לשלב ולהתאים ספריות שונות לפרוייקט שלהם בקלות.

קבוצת [Framework Interop][fig] הציעה ואישרה מספר המלצות עיצוב. לא כולן קשורות לעיצוב קוד,
אך אלו שכן הן [PSR-0][psr0], [PSR-1][psr1], [PSR-2][psr2] וגם [PSR-4][psr4]. המלצות אלה מהוות סט של כללים
אשר פרויקטים כגון Zend, Symfony, CakePHP, phpBB, AWS SDK, FuelPHP, Lithium, etc התחילו לאמץ. 
ניתן להשתמש בהן בפרויקטים שלכם או להמשיך ולקודד בסגנונכם האישי.

באופן אידיאלי, עדיף לכתוב קוד PHP אשר עומד בתקן ידוע. סטנדרט שכזה יכול להיות כל שילוב של PSR's, או אחת
מתקני הקידוד שנוצרו על ידי PEAR או Zend. באופן זה, מפתחים אחרים יוכלו לקרוא ולעבוד עם הקוד שלך בקלות ומערכות
אשר מיישמות את הרכיבים הנ"ל עדיין יכולות להיות בעלות סגנון עקבי גם אם הן מכילות רכיבי צד שלישי רבים.

* [למידע נוסף על PSR-0][psr0]
* [למידע נוסף על PSR-1][psr1]
* [למידע נוסף על PSR-2][psr2]
* [למידע נוסף על PSR-4][psr4]
* [למידע נוסף על תקני קידוד של PEAR][pear-cs]
* [למידע נוסף על תקני קידוד של Symfony][symfony-cs]

ניתן להיעזר ב- [PHP_CodeSniffer][phpcs] כדי לבדוק קוד אל מול כל אחת מההמלצות, וקיימים תוספים לעורכי טקסט רבים 
כגון [Sublime Text 2][st-cs] אשר נותנים משוב בזמן אמת.

ניתן לתקן את פריסת הקוד באופן אוטומטי ע"י שימוש באחד משני הכלים הבאים. הראשון שבהם הוא [PHP Coding Standards Fixer][phpcsfixer]
אשר מכיל בסיס קוד יציב ואמין. 
אפשרות נוספת היא [php.tools][phptools], שקודמה מאוד ע"י תוסף לעורך הטקסט [sublime-phpfmt][sublime-phpfmt]. 
העובדה שכלי זה חדש יותר, משמעותה מהירות ביצועים גבוהה יותר, משמע, תיקון קוד בזמן אמת באופן שוטף.

ניתן גם להריץ באופן ידני משורת הפקודה את התכנית phpcs:

    phpcs -sw --standard=PSR2 file.php

הפלט יציג שגיאות קוד והצעה לפתרון.
בנוסף, הוספת הפקודה הנ"ל ככלל git יכולה להיות שימושית מאוד.
בדרך זו, ענפים אשר מכילים הפרות תקן נבחר לא יכולים להירשם במאגר עד שהפרות אלו תוקנו.

עדיף להשתמש באנגלית עבור כל שמות הסימן ותשתיות הקוד. את ההערות ניתן לכתוב בכל שפה הניתנת לקריאה ע"י כל 
משתתפי הפרויקט בהווה תוך שיקול של גופים אחרים אשר עשויים לעבוד על תשתיות הקוד בעתיד.

[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
[phptools]: https://github.com/dericofilho/php.tools
[sublime-phpfmt]: https://github.com/dericofilho/sublime-phpfmt
