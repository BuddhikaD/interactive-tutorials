Lists דומות מאוד למערכים. הן יכולות להכיל כל סוג של משתנה, והן יכולות להכיל כמה משתנים שתרצו. ניתן גם לבצע איטרציה על רשימות בצורה פשוטה מאוד. הנה דוגמה לבנייה של רשימה.

    mylist = []
    mylist.append(1)
    mylist.append(2)
    mylist.append(3)
    print(mylist[0]) # prints 1
    print(mylist[1]) # prints 2
    print(mylist[2]) # prints 3

    # prints out 1,2,3
    for x in mylist:
        print(x)

גישה לאינדקס שאינו קיים יוצרת חריגה (שגיאה).

    mylist = [1,2,3]
    print(mylist[10])

Exercise
--------

בתרגיל זה, תצטרכו להוסיף מספרים ומחרוזות לרשימות הנכונות באמצעות שימוש בשיטת "append" של רשימות. עליכם להוסיף את המספרים 1,2, ו-3 לרשימת "numbers", ואת המילים 'hello' ו-'world' למשתנה strings.

תצטרכו גם למלא את המשתנה second_name עם השם השני ברשימת names, תוך שימוש באופרטור סוגריים `[]`. שימו לב כי האינדקס מתחיל מ-0, ולכן אם תרצו לגשת לפריט השני ברשימה, האינדקס שלו יהיה 1.