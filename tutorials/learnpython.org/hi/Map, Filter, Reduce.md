Map, Filter, और Reduce फ़ंक्शनल प्रोग्रामिंग के पैटर्न्स हैं। यह प्रोग्रामर (आप) को सरल, छोटे कोड लिखने की अनुमति देते हैं, बिना लूप्स और ब्रांचिंग जैसी बारीकियों की चिंता किए।

मूलतः, ये तीनों फ़ंक्शन आपको कई iterable पर एक फ़ंक्शन लागू करने की अनुमति देते हैं, एक ही बार में। `map` और `filter` Python में पहले से ही शामिल हैं (```__builtins__``` मॉड्यूल में) और इसके लिए कोई इम्पोर्ट की आवश्यकता नहीं होती। जबकि `reduce` को इम्पोर्ट करना पड़ता है क्योंकि यह ```functools``` मॉड्यूल में होता है। आइए हम समझते हैं कि ये सभी कैसे काम करते हैं, `map` से शुरू करते हैं।

#### Map
Python में `map()` फ़ंक्शन का निम्नलिखित सिंटैक्स है:

```map(func, *iterables)```

जहाँ ```func``` वह फ़ंक्शन है जो प्रत्येक अवयव पर `iterables` में लागू होगी। ध्यान दें कि `iterables` पर asterisk(```*```) है? इसका अर्थ है कि जितने भी iterable हो सकते हैं, अगर ```func``` को उतनी ही इनपुट आर्ग्युमेंट्स की आवश्यकता है। किसी उदाहरण को देखने से पहले, यह नोट करना महत्वपूर्ण है:

1. Python 2 में, `map()` फ़ंक्शन एक सूची लौटाता है। Python 3 में, फ़ंक्शन एक ```map object``` लौटाता है जो कि जनरेटर ऑब्जेक्ट होता है। परिणाम को सूची के रूप में प्राप्त करने के लिए, बिल्ट-इन `list()` फ़ंक्शन को map ऑब्जेक्ट पर कॉल किया जा सकता है। यानि ```list(map(func, *iterables))```
2. ```func``` को जितने आर्ग्युमेंट्स की आवश्यकता होती है, उन्हें ```iterables``` की सूची में होना चाहिए। 

आइए इन नियमों को निम्नलिखित उदाहरणों के साथ देखते हैं।

मान लीजिए मेरे पास मेरे पसंदीदा पालतू नामों की एक सूची (```iterable```) है, सभी छोटे अक्षरों में और मुझे उन्हें बड़े अक्षरों में चाहिए। पारंपरिक रूप से, सामान्य पायथन में, मैं कुछ इस तरह करूँगा:

    my_pets = ['alfred', 'tabitha', 'william', 'arla']
    uppered_pets = []

    for pet in my_pets:
        pet_ = pet.upper()
        uppered_pets.append(pet_)

    print(uppered_pets)

जो आउटपुट करेगा: ```['ALFRED', 'TABITHA', 'WILLIAM', 'ARLA']```

`map()` फ़ंक्शंस के साथ, यह न केवल आसान है, बल्कि यह भी अधिक लचीला है। मैं इसे सिर्फ इस तरह करता हूँ:

    # Python 3
    my_pets = ['alfred', 'tabitha', 'william', 'arla']

    uppered_pets = list(map(str.upper, my_pets))

    print(uppered_pets)

जो समान परिणाम देता है। ध्यान दें कि ऊपर बताए गए `map()` सिंटैक्स का उपयोग करते हुए, ```func``` इस मामले में ```str.upper``` है और ```iterables``` `my_pets` की सूची है - सिर्फ एक iterable। यह भी ध्यान दें कि हमने `str.upper` फ़ंक्शन को कॉल नहीं किया (जैसे कि ```str.upper()```), क्योंकि map फ़ंक्शन इसे `my_pets` सूची के _हर एक तत्व पर_ करता है।

एक और महत्वपूर्ण बात यह है कि ```str.upper``` फ़ंक्शन को परिभाषा के अनुसार केवल **एक** तर्क की आवश्यकता होती है इसलिए हमने उसे केवल **एक** iterable पास किया। तो, अगर आप जो फ़ंक्शन पास कर रहे हैं उसे दो, या तीन, या n आर्ग्युमेंट्स की आवश्यकता है, तो आपको दो, तीन, या n iterables उसे पास करने की आवश्यकता है। आइए इसे एक और उदाहरण के माध्यम से स्पष्ट करें।

मान लीजिए मेरे पास पहले से कहीं पर गणना की गई सर्कल क्षेत्रफल की एक सूची है, सभी पाँच दशमलव स्थानों में। और मुझे सूची के प्रत्येक तत्व को उसकी स्थिति दशमलव स्थानों तक राउंड करना है, अर्थात मुझे सूची के पहले तत्व को एक दशमलव स्थान तक राउंड करना है, दूसरे तत्व को दो दशमलव स्थान तक, तीसरे तत्व को तीन दशमलव स्थान तक, आदि। `map()` के साथ यह बहुत आसान है। आइए देखते हैं कैसे।

Python पहले से ही हमें `round()` बिल्ट-इन फ़ंक्शन प्रदान करता है जो दो आर्ग्युमेंट्स लेता है - उस संख्या को राउंड करना और उस संख्या को कितने दशमलव स्थानों तक राउंड करना है। चूंकि फ़ंक्शन को **दो** आर्ग्युमेंट्स की आवश्यकता है, हमें **दो** iterables पास करने की आवश्यकता है।

    # Python 3

    circle_areas = [3.56773, 5.57668, 4.00914, 56.24241, 9.01344, 32.00013]

    result = list(map(round, circle_areas, range(1, 7)))

    print(result)

क्या आप देख सकते हैं कि यह कितना लचीला है? क्या आप इस लचीलेपन की कल्पना कर सकते हैं?

```range(1, 7)``` फ़ंक्शंस `round` फ़ंक्शन के दूसरे आर्ग्युमेंट (प्रति iteration आवश्यक दशमलव स्थानों की संख्या) के रूप में कार्य करता है। जैसे ही ```map``` ```circle_areas``` पर संचालित होता है, पहले iteration के दौरान, ```circle_areas``` का पहला तत्व, ```3.56773```, और ```range(1,7)``` का पहला तत्व, ```1```, `round` पर पास होता है, जिससे यह वास्तव में ```round(3.56773, 1)``` बन जाता है। दूसरे iteration के दौरान, ```circle_areas``` का द्वितीय तत्व, ```5.57668``` और ```range(1,7)``` का दूसरा तत्व, ```2``` `round` पर पास होता है जिससे यह वास्तव में ```round(5.57668, 2)``` बन जाता है। यह तब तक होता है जब तक ```circle_areas``` की सूची समाप्त नहीं हो जाती।

आप सोच रहे होंगे: "अगर मैं पहला iterable से छोटा या बड़ा एक iterable पास करता हूँ तब क्या होगा? जैसे कि अगर मैं ```range(1, 3)``` या ```range(1, 9999)``` दूसरा iterable के रूप में पास करता हूँ तो क्या होगा?" और इसका उत्तर सरल है: कुछ नहीं! ठीक है, यह सच नहीं है। "कुछ नहीं" इस अर्थ में होता है कि ```map()``` फ़ंक्शन कोई भी अपवाद नहीं फेंकेगा, यह केवल तत्वों पर संचालित होगा जब तक कि उसे फ़ंक्शन के लिए दूसरा आर्ग्युमेंट नहीं मिल पाता, तब यह केवल रुक जाएगा और परिणाम लौटाएगा।

तो, उदाहरण के लिए, यदि आप ```result = list(map(round, circle_areas, range(1, 3)))``` का मूल्यांकन करते हैं, तो भी आपको कोई त्रुटि नहीं मिलेगी भले ही ```circle_areas``` की लंबाई और ```range(1, 3)``` की लंबाई अलग हों। बल्कि, यह है जो पायथन करता है: यह ```circle_areas``` के पहले तत्व को और ```range(1,3)``` के पहले तत्व को लेता है और इसे `round` पास करता है। ```round``` इसे मूल्यांकन करता है फिर परिणाम को सहेजता है। फिर यह दूसरे iteration में जाता है, ```circle_areas``` का दूसरा तत्व और ```range(1,3)``` का दूसरा तत्व, ```round``` इसे फिर से सहेजता है। अब, तीसरे iteration (```circle_areas``` के पास एक तीसरा तत्व है), पायथन ```circle_areas``` का तीसरा तत्व लेता है और फिर ```range(1,3)``` का तीसरा तत्व लेने की कोशिश करता है लेकिन चूंकि ```range(1,3)``` के पास तीसरा तत्व नहीं है, पायथन केवल रुक जाता है और परिणाम लौटाता है, जो इस मामले में केवल ```[3.6, 5.58]``` होगा।

आगे बढ़ें, इसे आजमाएं।

    # Python 3

    circle_areas = [3.56773, 5.57668, 4.00914, 56.24241, 9.01344, 32.00013]

    result = list(map(round, circle_areas, range(1, 3)))

    print(result)

यदि ```circle_areas``` की लंबाई दूसरे iterable से कम है तो भी यही प्रक्रिया होती है। पायथन केवल तभी रुक जाता है जब यह जोड़ने के लिए अगला तत्व नहीं पाता है।  

```map()``` फ़ंक्शन के हमारे ज्ञान को मजबूत करने के लिए, हम इसका उपयोग अपने eigenen custom ```zip()``` फ़ंक्शन को लागू करने के लिए करेंगे। ```zip()``` फ़ंक्शन एक ऐसा फ़ंक्शन है जो कई iterable को लेता है और फिर उनमें से प्रत्येक तत्वों के साथ एक tuple बनाता है। ```map()``` की तरह, Python 3 में, यह एक जनरेटर ऑब्जेक्ट देता है, जिसे आसानी से बिल्ट-इन ```list``` फ़ंक्शन का उपयोग करके सूची में परिवर्तित किया जा सकता है। नीचे दिए गए इंटरप्रेटर सत्र का उपयोग करें ```zip()``` के अंदर एक पकड़ प्राप्त करने के लिए इससे पहले कि हम ```map()``` के साथ इसे बनाएँ।

    # Python 3

    my_strings = ['a', 'b', 'c', 'd', 'e']
    my_numbers = [1, 2, 3, 4, 5]

    results = list(zip(my_strings, my_numbers))
    
    print(results)

एक बोनस के रूप में, अगर ```my_strings``` और ```my_numbers``` समान लंबाई में नहीं हैं तो ऊपर के सत्र में क्या होगा इसकी संभावना कर सकते हैं? नहीं? इसे आज़माएं! इनमें से किसी एक की लंबाई को बदलें।

अब अपने खुद के custom ```zip()``` फ़ंक्शन के लिए!

    # Python 3

    my_strings = ['a', 'b', 'c', 'd', 'e']
    my_numbers = [1, 2, 3, 4, 5]

    results = list(map(lambda x, y: (x, y), my_strings, my_numbers))

    print(results)

बस इसे देखें! हमें ```zip``` के समान परिणाम मिला है।

क्या आपने यह नोट किया कि मैंने यहाँ भी मानक तरीके से फ़ंक्शन बनाने की आवश्यकता नहीं पड़ी? ऐसा ही लचीलापन ```map()```, और सामान्य रूप से, पायथन है! मैंने सिर्फ एक ```lambda``` फ़ंक्शन का उपयोग किया। इसका अर्थ यह नहीं है कि मानक फ़ंक्शन परिभाषा विधि (```def function_name()```) का उपयोग नहीं कर सकते हैं, यह अभी भी है। मैंने सिर्फ कम कोड लिखना पसंद किया (यानी "Pythonic" बनना)।

भाषांतरण समाप्त। अब हम ```filter()``` की ओर बढ़ते हैं।

#### Filter
जबकि `map()` हर एक तत्व को iterable में फ़ंक्शन के माध्यम से पास करता है और सभी तत्वों के फ़ंक्शन से गुजरने के परिणाम को लौटाता है, ```filter()``` सबसे पहले फ़ंक्शन को boolean मान (सत्य या असत्य) लौटाने की आवश्यकता होती है और फिर यह iterable के हर एक तत्व को फ़ंक्शन के माध्यम से पास करता है, "छानता" हुआ केवल वे जो सत्य होते हैं। इसका निम्नलिखित सिंटैक्स है:

```filter(func, iterable)```

```filter()``` के संबंध में निम्नलिखित बातें नोट करने योग्य हैं:

1. ```map()``` के विपरीत, केवल एक iterable की आवश्यकता होती है।
2. ```func``` आर्ग्युमेंट को boolean प्रकार लौटाने की आवश्यकता होती है। अगर ऐसा नहीं होता, तो ```filter``` केवल पास किए गए ```iterable``` को ही लौटाता है। और यदि केवल एक iterable की आवश्यकता है, तो यह अव्यक्त है कि ```func``` को केवल एक आर्ग्युमेंट लेना चाहिए।
3. ```filter``` iterable के हर एक तत्व को ```func``` के माध्यम से पास करता है और केवल वे लौटाता है जो सत्य होते हैं। मुझे मतलब है, यह नाम में ही है -- एक "filter"।

आइए कुछ उदाहरण देखते हैं

निम्नलिखित एक सूची है (```iterable```) 10 छात्रों के केमिस्ट्री परीक्षा में स्कोर की। चलिए 75 से अधिक स्कोर वाले उन विद्यार्थियों को छानते हैं...`filter` का उपयोग करके।

    # Python 3
    scores = [66, 90, 68, 59, 76, 60, 88, 74, 81, 65]

    def is_A_student(score):
        return score > 75

    over_75 = list(filter(is_A_student, scores))

    print(over_75)

अगला उदाहरण एक palindrome डिटेक्टर होगा। एक "palindrome" एक शब्द, वाक्यांश, या अनुक्रम है जो पीछे से पढ़ने पर भी उसी प्रकार दिखता है। चलिए समभाषिक शब्दों को उन संभावित शब्दों की सूची (```iterable```) से छानते हैं।

    # Python 3
    dromes = ("demigod", "rewire", "madam", "freer", "anutforajaroftuna", "kiosk")

    palindromes = list(filter(lambda word: word == word[::-1], dromes))

    print(palindromes)

जो आउटपुट करता है ```['madam', 'anutforajaroftuna']```.

काफी अच्छा, है ना? अंततः, ```reduce()```

#### Reduce
```reduce``` एक फ़ंक्शन **दो तर्कों के** को क्रमिक रूप से एक iterable के तत्वों पर लागू करता है, संभवतः शुरू में एक आरंभिक तर्क के साथ। इसका निम्नलिखित सिंटैक्स है:

```reduce(func, iterable[, initial])```

जहां ```func``` वह फ़ंक्शन है जिस पर ```iterable``` के हर एक तत्व को क्रमिक रूप से लागू किया जाता है, और ```initial``` वह आरंभिक मान है जो गणना में ```iterable``` के तत्वों के पहले स्थान पर रखा जाता है और जब ```iterable``` खाली होता है तब एक डिफ़ॉल्ट के रूप में कार्य करता है। निम्नलिखित को ```reduce()``` के संबंध में नोट किया जाना चाहिए:
1. ```func``` को दो तर्क चाहिए, जिनमें से पहला ```iterable``` का पहला तत्व होता है (यदि ```initial``` नहीं दिया गया है) और दूसरा ```iterable``` का दूसरा तत्व होता है। अगर ```initial``` दिया गया है, तो यह ```func``` का पहला तर्क बन जाता है और ```iterable``` का पहला तत्व दूसरा तर्क बन जाता है।
2. ```reduce``` "घटाता" (मुझे माफ करना) है ```iterable``` को एक केवलिका में। 

जैसे हमेशा, आइए कुछ उदाहरण देखें।

आइए Python के बिल्ट-इन ```sum()``` फ़ंक्शन का अपना संस्करण बनाते हैं। ```sum()``` फ़ंक्शन उस iterable के सभी items का योग लौटाता है जो इसे पास किया जाता है। 

    # Python 3
    from functools import reduce

    numbers = [3, 4, 6, 9, 34, 12]

    def custom_sum(first, second):
        return first + second

    result = reduce(custom_sum, numbers)
    print(result)

परिणाम, जैसा कि आप अपेक्षा करेंगे, ```68``` है।

तो, क्या हुआ?

जैसा कि हमेशा, यह सब iteration के बारे में है: ```reduce``` पहले और दूसरे तत्व को ```numbers``` में लेता है और उन्हें क्रमशः ```custom_sum``` में पास करता है। ```custom_sum``` उनका योग गणना करता है और इसे ```reduce``` को लौटा देता है। ```reduce``` फिर उस परिणाम को लेता है और ```custom_sum``` के पहले तत्व के रूप में लागू करता है और ```numbers``` के अगले तत्व (तीसरे) को ```custom_sum``` के दूसरे तत्व के रूप में लेता है। यह इस प्रकार लातार (क्रमिक रूप से) करता है जब तक ```numbers``` समाप्त नहीं हो जाता।

आइए देखते हैं कि जब मैं ‌```initial``` वैल्यु का उपयोग करता हूँ तो क्या होता है।

    # Python 3
    from functools import reduce

    numbers = [3, 4, 6, 9, 34, 12]

    def custom_sum(first, second):
        return first + second

    result = reduce(custom_sum, numbers, 10)
    print(result)

परिणाम, जैसा कि आप अपेक्षा करेंगे, ```78``` है क्योंकि ```reduce``` शुरूआती रूप से ```10``` का उपयोग ```custom_sum``` के पहले तर्क के रूप में करता है।

यही है Python के Map, Reduce, और Filter के बारे में। नीचे दिए गए अभ्यास को आजमाएँ ताकि आप प्रत्येक फ़ंक्शन की अपनी समझ को सत्यापित कर सकें।

अभ्यास
--------

इस अभ्यास में, आप टूटे हुए कोड को ठीक करने के लिए प्रत्येक ```map```, ```filter```, और ```reduce``` का उपयोग करेंगे।