### Switch-case alternatifleri

###### Switch-case Python'da olmayan bir sey. Ama programlamak her zaman yaraticilikla dolu oldugu icin switch-case keywords olmadan da yapilabilmenin (bilinen) 3 yolu var:

: 1) Dictionary ile simüle edilebilir:
```python
switch_dictionary = {
    0: 'sifir',
    1: 'bir',
    2: 'iki',
    3: 'üc'
}
zahl = int(input("Lütfen bir sayi girin: "))
print(switch_dictionary.get(sayi, 'Verilen sayi 0 ile 3 arasinda olmalidir!'))
```

: 2) If-else-elif ile de yapilabilir:

```python
def switch_if(sayi):
    if sayi == 0:
        return 'Sifir'
    elif sayi == 1:
        return 'Bir'
    elif sayi == 2:
        return 'Iki'
    elif sayi == 3:
        return 'Üc'
    else:
        return 'Verilen sayi 0 ile 3 arasinda olmalidir!'
sayi = int(input("Lütfen bir sayi girin: "))
print(switch_if(sayi))
```

: 3) ve son olarak class'lar ile yapilabiliyor:

```python
class Switch(object):
    def __init__(self):
        # Bütün olasilikli veriler burada kaydedilir.
        self.cases = []
        # Herhangi bir durum girildiginde kaydedilir
        self.case_matched = False
    def add_case(self, value, callback, breaks=True):
        # Dahili self.cases listesinin sonuna bir olasilik ekler.
        self.cases.append({
            "value": value,
            "callback": callback,
            "breaks": breaks
        })
    
    def case(self, value):
        # Ara sonuclari kaydeder (temporary)      
        results = []
        for case in self.cases:
            # önceki bir olasiligin zaten gelip gelmediğini kontrol eder
            # veyahut mevcut vakanın gelip gelmediğini kontrol eder
            if self.case_matched == True or value == case["value"]:
                self.case_matched = True
                # Geçerli vaka için geri aramanın sonucu kaydedilir
                results.append(case["callback"]())
                # Gecerli durum için break'ler True olarak ayarlanırsa döngü sona erer
                if case["breaks"]:
                    break
        self.case_matched = False
        return results
switch = Switch()
case_1 = lambda : "Bir"
case_2 = lambda : "Iki"
case_3 = lambda : "Üc"
switch.add_case(1, case_1, False)
switch.add_case(2, case_2, False)
switch.add_case(3, case_3, False)
print(switch.case(1))
print(switch.case(2))
print(switch.case(3))
```
