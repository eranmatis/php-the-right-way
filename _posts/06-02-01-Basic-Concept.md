---
isChild: true
anchor:  basic_concept
---

## הבנה בסיסית {#basic_concept_title}

ניתן להדגים את הנושא באמצעות דוגמא פשוטה ותמימה.

בדוגמא זו יש לנו מחלקת `Database` אשר עבורה נדרש מתאם אשר "מדבר" עם מאגר הנתונים. אנו יוצרים מופע של מתאם זה
באמצעות בנאי ויוצרים בו תלות קשיחה. דבר זה הופך את מלאכת הבדיקה לקשה - משמע, מחלקת `Database` נמצאת בצימוד חזק
למתאם.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct()
    {
        $this->adapter = new MySqlAdapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

קוד זה יכול לעבור התאמה לשימוש בהזרקת תלויות וכך להחליש את התלות.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(MySqlAdapter $adapter)
    {
        $this->adapter = $adapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

כעת אנו נותנים למחלקה `Database` את התלות שלה במקום לתת לה את האחריות על יצירתה בעצמה. אנו יכולים אפילו ליצור
פונקציה אשר יודעת לקבל ארגומנט של התלות ולבצע השמה בדרך זו, או אם הרשאת ה-`$adapter` הייתה `public`, 
ניתן לבצע השמה באופן ישיר.
