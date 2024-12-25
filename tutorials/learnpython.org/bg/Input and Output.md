Взимането на вход и показването на изход по желания начин играе важна роля в интерактивното програмиране. Така че нека се фокусираме върху входа и изхода на различни видове данни.

###raw_input()
Това се използва за взимане на вход, докато не се достигне краят на реда. Обърнете внимание, че не трябва да има никакви пространства. Взимането на вход завършва с нов ред символ и ако има пространства във входния ред, това води до грешка.

    # Принтира получения вход от stdin
    astring=raw_input()# въведете hello като вход
    print raw_input()

След като вземем входа, можем да го преобразуваме в желания от нас тип данни, използвайки функции като int(), float(), str().

    num=int(raw_input())
    print num
    decimalnum=raw_input()
    decimalnum=float(raw_input()
    print decimalnum

###input()
Това се използва особено за въвеждане на цели числа. Предимството на input() пред raw_input() може да бъде изяснено със следния пример.

    #въведете 2*2 като вход
    a=input()
    b=raw_input() #имайте предвид, че int(raw_input()) води до грешка
    print a #принтира 4
    print b #принтира 2*2

###как да вземем два или повече видове данни от един ред, разделени с пространства?
Тук използваме функциите split() и map().

    #въведете две цели числа в първия ред и повече от две цели числа в третия ред
    a, b = map(int, raw_input().split())
    array = raw_input().split()
    sum = 0
    for each in array:
        sum = sum + int(each)
    print(a, b, sum)  # принтира първите две цели числа от първия ред и сумата на целите числа от втория ред

###Форматиране на изхода
Вероятно вече сте забелязали, че командата print автоматично вмъква нов ред. Използването на запетая, както в горния код, принтира стойностите в един ред, разделени с място. Модулът sys предоставя различни функции за форматиране на изхода, но тук ще научим как да използваме основни знания за форматиране, за да изведем по желания начин. Нека видим няколко примера за форматиране на изхода.

    a = 5
    b = 0.63
    c = "hello"
    print "a е: %d, b е %0.4f, c е %s" % (a, b, c)

Изходът трябва да е самообяснителен.

Упражнение
--------

Напишете програма, която пита потребителя да въведе името си, възрастта и страната. Програмата след това трябва да изведе съобщение, което включва тази информация в изречение. Програмата трябва да включва:

1. Вземане на име чрез `raw_input()`.
2. Вземане на възраст чрез `input()`, и преобразуването му в цяло число.
3. Вземане на име на страна чрез `raw_input()`.
4. Форматиране на изхода за показване на изречение, което включва името, възрастта и страната.

Програмата трябва да демонстрира управление на входа и форматиране на низове в Python.