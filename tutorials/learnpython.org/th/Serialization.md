Python มีไลบรารี JSON ที่สร้างขึ้นมาในตัวเพื่อการเข้ารหัสและถอดรหัส JSON

ใน Python 2.5 โมดูล simplejson ถูกใช้งาน, แต่ใน Python 2.7 โมดูล json ถูกใช้งาน. เนื่องจาก interpreter นี้ใช้ Python 2.7, เราจะใช้งาน json

เพื่อที่จะใช้งานโมดูล json, ก่อนอื่นจะต้อง import:

    import json

มีสองรูปแบบพื้นฐานสำหรับข้อมูล JSON. ไม่ว่าจะเป็นในรูปแบบสตริงหรือโครงสร้างข้อมูลอ็อบเจ็กต์. โครงสร้างข้อมูลอ็อบเจ็กต์, ใน Python, ประกอบด้วย lists และ dictionaries ที่ซ้อนกัน. โครงสร้างข้อมูลอ็อบเจ็กต์อนุญาตให้ใช้ methods ของ python (สำหรับ lists และ dictionaries) ในการเพิ่ม, ลิสต์, ค้นหา และลบองค์ประกอบจากโครงสร้างข้อมูล. รูปแบบสตริงมักจะใช้ในการส่งข้อมูลไปยังโปรแกรมอื่นหรือโหลดเข้าโครงสร้างข้อมูล.

ในการโหลด JSON กลับสู่โครงสร้างข้อมูล, ใช้เมธอด "loads". เมธอดนี้รับสตริงและเปลี่ยนให้กลับเป็นโครงสร้างข้อมูลอ็อบเจ็กต์ json:

    import json 
    print(json.loads(json_string))

ในการเข้ารหัสโครงสร้างข้อมูลเป็น JSON, ใช้เมธอด "dumps". เมธอดนี้รับอ็อบเจ็กต์และคืนค่าเป็นสตริง:

    import json
    json_string = json.dumps([1, 2, 3, "a", "b", "c"])
    print(json_string)

Python สนับสนุนวิธีการทำซีเรียลไลส์ข้อมูลที่เป็นกรรมสิทธิ์ของ Python ชื่อว่า pickle (และมีทางเลือกที่เร็วกว่าเรียกว่า cPickle).

คุณสามารถใช้งานมันได้ในลักษณะเดียวกัน

    import pickle
    pickled_string = pickle.dumps([1, 2, 3, "a", "b", "c"])
    print(pickle.loads(pickled_string))

Exercise--------

เป้าหมายของแบบฝึกหัดนี้คือการพิมพ์สตริง JSON ที่มีคู่คีย์-ค่าที่ว่า "Me" : 800 ถูกเพิ่มเข้าไปในนั้น.