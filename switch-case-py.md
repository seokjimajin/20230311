ve son olarak class'lar ile yapilabiliyor:

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
