---
layout: page
title:  Design Patterns
sitemap: true
---

# תבניות עיצוב

ישנן אינספור דרכים לעצב ולבנות את הקוד ואת הפרויקט לאפליקצייה שלכם ואתם יכולים להקדיש מחשבה מעטה או רבה בנושא
ארכיטקטורת הפרויקטת אך בדרך כלל יישום של תבניות עיצוב שכיחות הוא רעיון טוב. בדרך זו יהיה קל יותר לנהל את הקוד
וכמובן נוח יותר לאחרים להבין.

* [ארכיטקטורות תבניות ב-Wikipedia](https://en.wikipedia.org/wiki/Architectural_pattern)
* [עיצוב תבניות תוכנה ב-Wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)
* [אוסף של דוגמאות יישום](https://github.com/domnikl/DesignPatternsPHP)

## Factory - מפעל

אחת מתבניות העיצוב השימושיות ביותר היא תבנית המפעל. בתבנית זו, מחלקה יוצרת את העצם בו אנו רוצים לעשות שימוש.
קחו למשל את הדוגמא הבאה של תבנית המפעל:

{% highlight php %}
<?php
class Automobile
{
    private $vehicleMake;
    private $vehicleModel;

    public function __construct($make, $model)
    {
        $this->vehicleMake = $make;
        $this->vehicleModel = $model;
    }

    public function getMakeAndModel()
    {
        return $this->vehicleMake . ' ' . $this->vehicleModel;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// המפעל מייצר את הרכב
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->getMakeAndModel()); // outputs "Bugatti Veyron"
{% endhighlight %}

הקוד הנ"ל עושה שימוש במפעל על מנת לייצר עצם מסוג Automobile. יש שני יתרונות אפשריים מבניית הקוד בדרך זו;
היתרון הראשון הוא שאם יש צורך לשכתב, לשנות שם או להחליף את מחלקת Automobile בשלב מאוחר יותר, ניתן לעשות זאת
תוך שינוי של הקוד במפעל עצמו במקום בכל מקום בו יש שימוש במחלקה Automobile בפרויקט.
היתרון השני האפשרי טמון ביכולת לריכוז העבודה המתבצעת ביצירת Automobile בתוך מחלקת המפעל במקום לחזור על הקוד 
פעמים רבות בכל פעם בו אנו רוצים ליצור מופע חדש.

השימוש בתבנית המפעל אינה תמיד הכרחית (או נבונה). דוגמת הקוד הבאה כה פשוטה עד שמפעל פשוט יוסיף מורכבות שאינה 
נחוצה במקום זה. עם זאת, במידה ואתם יוצרים פרוייקטים גדולים ו/או מורכבים, אתם עשויים לחסוך לעצמכם צרות רבות בהמשך
הדרך ע"י שימוש בתבניות מפעלים.

* [על תבנית המפעל ב-Wikipedia](https://en.wikipedia.org/wiki/Factory_pattern)

## Singleton - סינגלטון (קלף-בודד)

כאשר מאפיינים אפליקציות web, לעיתים נרצה משיקולי ארכיטקטורה ועקרונות מנחים לאפשר גישה למחלקה מסויימת דרך 
מופע אחד ואחד בלבד. תבנית הסינגלטון מאפשרת לנו לבצע בדיוק את זה.

{% highlight php %}
<?php
class Singleton
{
    /**
     * @var Singleton נקודת הייחוס למופע ה-*Singleton* של מחלקה זו
     */
    private static $instance;
    
    /**
     * מחזיר את מופע ה-*Singleton* של מחלקה זו.
     *
     * @return Singleton The *Singleton* instance.
     */
    public static function getInstance()
    {
        if (null === static::$instance) {
            static::$instance = new static();
        }
        
        return static::$instance;
    }

    /**
     * בנאי מוגן המונע יצירת מופע חדש של ה-*Singleton*
     *  באמצעות האופרטור `new` מחוץ למחלקה זו.
     */
    protected function __construct()
    {
    }

    /**
     * מתודת השכפול היא פרטית כדי למנוע שכפול המופע של ה-*Singleton*
     *
     * @return void
     */
    private function __clone()
    {
    }

    /**
     * מתודת  unserialize פרטית למניעת פעולת unserializing של מופע ה-*Singleton*
     *
     * @return void
     */
    private function __wakeup()
    {
    }
}

class SingletonChild extends Singleton
{
}

$obj = Singleton::getInstance();
var_dump($obj === Singleton::getInstance());             // bool(true)

$anotherObj = SingletonChild::getInstance();
var_dump($anotherObj === Singleton::getInstance());      // bool(false)

var_dump($anotherObj === SingletonChild::getInstance()); // bool(true)
{% endhighlight %}

הקוד הנ"ל מיישם את תבנית הסינגלטון באמצעות [משתנה *סטטי*](http://php.net/language.variables.scope#language.variables.scope.static) ופונקציית היצירה הסטטית `getInstance()`.
אנא שימו לב לנקודות הבאות:

* הבנאי [`__construct()`](http://php.net/language.oop5.decon#object.construct) מוגדר כמוגן כדי למנוע יצירת מופע 
חדש של מחלקה זו באמצעות האופרטור `new`.
* פונקציית הקסם [`__clone()`](http://php.net/language.oop5.cloning#object.clone) מוגדרת כפרטית כדי למנוע את שכפול המופע
באמצעות האופרטור [`clone`](http://php.net/language.oop5.cloning).
* פונקציית הקסם [`__wakeup()`](http://php.net/language.oop5.magic#object.wakeup) מוגדרת כפרטית כדי למנוע unserializing
 של המופע ממחלקה זו באמצעות הפונקצייה הגלובלית [`unserialize()`](http://php.net/function.unserialize).
* מופע חדש נוצר באמצעות [צימוד סטטי מאוחר](http://php.net/language.oop5.late-static-bindings) בפונקציית היצירה הסטטית 
`getInstance()` עם מילת המפתח `static`. דבר זה מאפשר יצירת רמה שניה למחלקה `Singleton` (הורשה) לפי הדוגמא.

תבנית הסינגלטון שימושית במצבים בהם אנו רוצים לוודא שקיים רק מופע אחד של מחלקה מסויימת בכל מעגל החיים של 
אפליקציית הרשת. מצבים כגון אלה בדרך כלל מופיעים כאשר יש לנו עצמים גלובליים (לדוגמא מחלקת קונפיגורצייה) או משאב
שיתופי (לדוגמא, תור אירועים).

צריך לנקוט משנה זהירות כאשר משתמשים בתבנית הסינגלטון, מפאת טבעה של תבנית זו המקנה לאפליקצייה התנהגות גלובלית
ומקשה יותר על יכולת הבדיקות. ברוב המקרים, הזרקת תלויות יכולה (ועדיפה) להחליף את השימוש בתבנית הסינגלטון.
שימוש בהזרקת תלויות חוסך לנו צימוד מיותר בעיצוב האפליקצייה. העצם אשר משתמש במשאב המשותף או הגלובלי אינו דורש
כל ידע אודות מחלקה המוגדרת באופן ברור וייעודי לכך.

* [תבנית הסינגלטון ב-Wikipedia](https://en.wikipedia.org/wiki/Singleton_pattern)

## Strategy - אסטרטגיה

באמצעות תבנית האסטרטגיה ניתן לכמס משפחות אלגוריתמים מסויימות אשר מופעלות באמצעות מחלקה אשר אחראית
על יצירת המופע של אלגוריתם מסוים שאין לו ידע על היישום בפועל. ישנן מספר וריאציות לתבנית האסטרטגיה, הפשוטה מהן
מפורטת להלן:

דוגמת הקוד הראשונה מציגה משפחת אלגוריתמים; ייתכן שנרצה לבצע פעולת סריאליזציה למערך, מעט JSON או אולי רק 
מערך המכיל מידע:

{% highlight php %}
<?php

interface OutputInterface
{
    public function load();
}

class SerializedArrayOutput implements OutputInterface
{
    public function load()
    {
        return serialize($arrayOfData);
    }
}

class JsonStringOutput implements OutputInterface
{
    public function load()
    {
        return json_encode($arrayOfData);
    }
}

class ArrayOutput implements OutputInterface
{
    public function load()
    {
        return $arrayOfData;
    }
}
{% endhighlight %}

פעולת הכימוס (encapsulation) של האלגוריתמים הנ"ל אנו מוודאים שמפתחים אחרים העושים שימוש בקוד יוכלו להוסיף
מימושים חדשים מבלי להשפיע על קוד הלקוח הקיים.

ניתן לראות כיצד כל מחלקת 'פלט' מיישמת ממשק 'OutputInterface'. - דבר זה משרת שתי מטרות, בראשונה הדבר מהווה חוזה פשוט
וברור אשר חייב להיות ממומש ע"י כל מחקה אשר עושה שימוש בו. בשנית, וכפי שנראה בפרק הבא, השימוש בממשק משותף 
מאפשר לנו גישה ל-[Type Hinting](http://php.net/language.oop5.typehinting) אשר נותן לנו כלי לבדיקה שאכן הלקוח אשר עושה שימוש
בהתנהגות זו הוא מהסוג הנכון ובמקרה זה מהסוג 'OutputInterface'.

דוגמת הקוד הבאה מדגישה כיצד מחלקת לקוח יכולה לעשות שימוש באלגוריתמים הללו ואפילו לשפר ולהתאים את התנהגותם
בשעת ריצה:

{% highlight php %}
<?php
class SomeClient
{
    private $output;

    public function setOutput(OutputInterface $outputType)
    {
        $this->output = $outputType;
    }

    public function loadOutput()
    {
        return $this->output->load();
    }
}
{% endhighlight %}

למחלקת הלקוח בדוגמה יש שדה פרטי אשר חייב להיות מושם בשעת ריצה לערך מהסוג 'OutputInterface'.
לאחר השמת השדה, יוצאת קריאה לפונקציה loadOutput() אשר בתורה יוזמת קריאה לפונקציה load() במחלקת האלגוריתם שנבחרה לפי
ערך הסוג שנבחר `$outputType`.

{% highlight php %}
<?php
$client = new SomeClient();

// Want an array?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Want some JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();

{% endhighlight %}

* [על תבנית האסטרטגיה ב-Wikipedia](http://en.wikipedia.org/wiki/Strategy_pattern)

## Front Controller - בקר קדמי

תבנית הבקר הקדמי, או המפקח הקדמי מתארת מצב בו קיימת נקודת גישה אחת ויחידה לאפליקצייה שלנו (לדוגמא, index.php)
אשר מטפלת בכל הבקשות. הקוד בתבנית אחראי על טעינת כל הרכיבים התלויים, עיבוד הבקשה ושליחת התשובה לדפדפן הלקוח.
תבנית הבקר הקדמי יכולה להועיל לנו ולעודד שיטת קידוד מודולרית אשר מספקת לנו מיקום מרכזי לעגן בו את הקוד אשר
אמור לרוץ בכל בקשה (לדוגמא, סניטציה של קוד).

* [על תבנית הבקר הקדמי ב-Wikipedia](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller - מודל, תצוגה, בקר

תבנית מודל, תצוגה, בקר (MVC) וקרובות המשפחה שלה HMVC ו- MVVM מאפשרות לנו לחלק את הקוד שלנו לעצמים לוגיים
אשר משרתים מטרה ספציפית. המודל משמש שכבת גישה למידע אשר בה המידע הולך וחוזר בפורמטים השימושיים לאפליקצייה.
הבקרים מטפלים בבקשות,מעבדים את המידע המושב מהמודלים וטוענים תצוגות לשליחה ללקוח.
התצוגות הן תבניות (markup, xml, etc) אשר נשלחות לדפדפן הלקוח.

תבנית ה-MVC היא התבנית השימושית ביותר [במערכות ה-PHP](https://github.com/codeguy/php-the-right-way/wiki/Frameworks) הנפוצות כיום 

למדו עוד אודות תבנית ה-MVC ותבניות קשורות:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
