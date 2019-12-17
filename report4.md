                    Лабораторна робота №4     

Автор: Коломійченко Богдан Сергійович
Група:ІПЗ-13
Варіант:7
                                                      Завдання
1.	Обчислити значення функції у, розвинувши функцію sh(x) у ряд Тейлора. Аргумент х змінюється від 0 до 3 з кроком 0.5. Визначити похибку 

def arctg(x,acc):
    q=1
    res=0
    for i in range (1, acc+1, 2):
        res+=q* (x**i/i)
        q*= -1
    return res

x=0
acc=  int(input('Введіть точність '))
while x<1:
    y=arctg(x, acc) + arctg(2*x,acc)
    print(f"x = {x}: y={y}")
    x+=0.5

while x<=3:
    y= arctg(x,acc) /arctg(x-5,acc)
    print(f"x = {x}: y={y}")
    x += 0.5
