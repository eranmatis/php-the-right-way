---
isChild: true
title:   Interacting with Databases
anchor:  databases_interacting
---

## אינטראקציה עם מאגרי מידע {#databases_interacting_title}
כאשר מפתחים מתחילים לראשונה ללמוד PHP, הם לעתים קרובות מערבבים את האינטראקציה של מסד הנתונים שלהם עם
שכבת לוגיקת התצוגה, באמצעות קוד שעשוי להיראות כך:

{% highlight php %}
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
?>
</ul>
{% endhighlight %}

זוהי פרקטיקה רעה מכל מיני סיבות, בעיקר כי קשה לאתר באגים, קשה לבדוק, הקוד קשה לקריאה אשר 
עלול להציג שדות רבים, אם לא נשים שם מגבלה.

כמובן שקיימים פתרונות נוספים - תלוי בהעדפתכם [OOP](/#object-oriented-programming) או
[functional programming](/#functional-programming) - אך עדיין חובה שתהיה הפרדה.

שקלו את הצעד הבסיסי ביותר:

{% highlight php %}
<?php
function getAllFoos($db) {
    return $db->query('SELECT * FROM table');
}

foreach (getAllFoos($db) as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // BAD!!
}
{% endhighlight %}

זוהי התחלה טובה. פצלו את שתי הפונקציות הנ"ל לשני קבצים נפרדים וקיבלתם הפרדה נקייה.

צרו מחלקה אשר בה תמקמו את אותה הפונקצייה וקיבלת "מודל" (Model). צרו קובץ `.php` פשוט אשר יכיל את התצוגה הלוגית 
קיבלת "תצוגה" (View), אשר  מקרבת אותנו מאוד ל-[MVC] - ארכיטקטורת OOP מקובלת וידועה [למערכות רבות](/#frameworks)..

**foo.php**

{% highlight php %}
<?php
$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8', 'username', 'password');

// צרף את המודל
include 'models/FooModel.php';

// צור את המופע
$fooModel = new FooModel($db);
// Get the list of Foos
$fooList = $fooModel->getAllFoos();

// צרף את התצוגה
include 'views/foo-list.php';
{% endhighlight %}


**models/FooModel.php**

{% highlight php %}
<?php
class FooModel
{
    protected $db;

    public function __construct(PDO $db)
    {
        $this->db = $db;
    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
{% endhighlight %}

**views/foo-list.php**

{% highlight php %}
<?php foreach ($fooList as $row): ?>
    <?= $row['field1'] ?> - <?= $row['field1'] ?>
<?php endforeach ?>
{% endhighlight %}

למעשה, פעולה זו זהה למה שרוב המערכות אקיימות מבצעות, אם כי מעט יותר בצורה ידנית. יכול להיות שלא יהיה צורך 
לבצע את הפרדה זו בכל פעם, אך עירוב של יותר מדי לוגיקות תצוגה עם גישות למאגר המידע יכול להוות בעיה אמיתית
אם בעתיד נרצה לשלב [יחידה-בדיקה (unit-test)](/#unit-testing) באפליקצייה.

באתר [PHPBridge] יש דף מצויין [Creating a Data Class] אשר מכסה נושא זהה כמעט לגמרי. מידע זה מומלץ למפתחים אשר
רק מתחילים להתרגל לקונספט של אינטראקציה עם מאגרי מידע.

[MVC]: http://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488
[PHPBridge]: http://phpbridge.org/
[Creating a Data Class]: http://phpbridge.org/intro-to-php/creating_a_data_class
