يستخدم بايثون المنطق البولياني لتقييم الشروط. تُعاد القيم البوليانية True وFalse عند مقارنة أو تقييم تعبير. على سبيل المثال:

x = 2
print(x == 2) # يطبع True
print(x == 3) # يطبع False
print(x < 3) # يطبع True

لاحظ أن تعيين المتغير يتم باستخدام علامة يساوي واحدة "="، بينما تتم المقارنة بين متغيرين باستخدام علامة يساوي مزدوجة "==". يتم الإشارة إلى معامل "غير متساوي" بـ "!=". 

### عوامل التشغيل البوليانية

تسمح عوامل التشغيل البوليانية "and" و"or" ببناء تعبيرات بوليانية معقدة، على سبيل المثال:

    name = "John"
    age = 23
    if name == "John" and age == 23:
        print("اسمك هو John، وأنت أيضًا تبلغ من العمر 23 عامًا.")

    if name == "John" or name == "Rick":
        print("اسمك إما John أو Rick.")

### عامل التشغيل "in"

يمكن استخدام عامل التشغيل "in" للتحقق مما إذا كان كائن محدد موجودًا داخل حاوية كائنات قابلة للتكرار، مثل قائمة:

    name = "John"
    if name in ["John", "Rick"]:
        print("اسمك إما John أو Rick.")

تستخدم بايثون المسافة البادئة لتحديد كتل الكود، بدلاً من الأقواس. المسافة البادئة القياسية في بايثون هي 4 مسافات، على الرغم من أن علامات التبويب وأي حجم مسافة آخر ستعمل، طالما كان متسقًا. لاحظ أن كتل الكود لا تحتاج إلى أي إغلاق. 

إليك مثال لاستخدام عبارة "if" في بايثون باستخدام كتل الكود:

    statement = False
    another_statement = True
    if statement is True:
        # تنفيذ شيء ما
        pass
    elif another_statement is True: # else if
        # تنفيذ شيء آخر
        pass
    else:
        # تنفيذ شيء مختلف
        pass

على سبيل المثال:

    x = 2
    if x == 2:
        print("x يساوي اثنان!")
    else:
        print("x لا يساوي اثنين.")

يتم تقييم البيان على أنه صحيح إذا كان أحد ما يلي صحيحًا:
1. تم تقديم المتغير البولياني "True"، أو حسابه باستخدام تعبير مثل مقارنة حسابية.
2. يتم تمرير كائن لا يعتبر "فارغًا".

إليك بعض الأمثلة على الكائنات التي تعتبر فارغة:
1. سلسلة فارغة: ""
2. قائمة فارغة: []
3. الرقم صفر: 0
4. المتغير البولياني الكاذب: False

### عامل التشغيل 'is'

على عكس عامل التشغيل يساوي المزدوج "=="، لا يطابق عامل التشغيل "is" قيم المتغيرات بل المثيلات ذاتها. على سبيل المثال:

    x = [1,2,3]
    y = [1,2,3]
    print(x == y) # يطبع True
    print(x is y) # يطبع False

### عامل التشغيل "not"

يؤدي استخدام "not" قبل تعبير بولياني إلى عكسه:

    print(not False) # يطبع True
    print((not False) == (False)) # يطبع False

Exercise
--------

قم بتغيير المتغيرات في القسم الأول بحيث يتم تقييم كل عبارة "if" على أنها True.