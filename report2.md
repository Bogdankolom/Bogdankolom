    Лабораторна робота №2     

Автор:Коломійченко Богдан Сергійович
Група:ІПЗ-13
Варіант:7




Прізвище:Коломійчненко Богдан Сергійович
Місце проживання:Київ

                           Завдання 

import math

res = 0
accuracy = 0


def type1(): 
    global res
    ticker = 0  
    if 0 < x < math.pi: 
        res = math.sin(x)
        print("Формула - sin(x)", end="\n\n")
        print_result()
        ticker = 1
    if math.pi < x < (3 * math.pi) / 2:  
        res = math.cos(x)
        print("Формула - cos(x)", end="\n\n")
        print_result()
        ticker = 1
    if (3 * math.pi) / 2 < x < 2 * math.pi: 
        res = math.sin(x) / math.cos(x)
        print("Формула - sin(x) / cos(x)", end="\n\n")
        print_result()
        ticker = 1
    if ticker == 0:
        print("Введене число не підходить до вимог. Виконання завершено.")


def type2():  
    global res
    if 0 < x < math.pi:  
        res = math.sin(x)
        print("Формула - sin(x)", end="\n\n")
        print_result()
    else:
        if math.pi < x < (3 * math.pi) / 2:  
            res = math.cos(x)
            print("Формула - cos(x)", end="\n\n")
            print_result()
        else:
            if (3 * math.pi) / 2 < x < 2 * math.pi:
                res = math.sin(x) / math.cos(x)
                print("Формула - sin(x) / cos(x)", end="\n\n")
                print_result()
            else:
                print("Введене число не підходить до вимог. Виконання завершено.")


def type3():
    global res
    if 0 < x < math.pi: 
        res = math.sin(x)
        print("Формула - sin(x)", end="\n\n")
        print_result()
    elif math.pi < x < (3 * math.pi) / 2: 
        res = math.cos(x)
        print("Формула - cos(x)", end="\n\n")
        print_result()
    elif (3 * math.pi) / 2 < x < 2 * math.pi: 
        res = math.sin(x) / math.cos(x)
        print("Формула - sin(x) / cos(x)", end="\n\n")
        print_result()
    else:
        print("Введене число не підходить до вимог. Виконання завершено.")


def print_result(): 
    global accuracy
    while True:
        try:
            accuracy = int(input("Оберіть кількість знаків після коми (зазвичай доступно не більше 20: "))
            break
        except ValueError:
            print("Некорректна відповідь")
            continue
    print("Результат в радіанах - " + str(round(res, accuracy)))
    print("Результат в градусах - " + str(round(math.degrees(res), accuracy)))


print("ІПЗ-13, Коломійченко Богдан Сергійович")
print("Лабораторна робота 2")

print("Обчислення функції залежно від значення константи")

while True:
    try:  
        x = float(input("Введіть значення X: ")) 
        break
    except ValueError:
        print("Некоректне значення")


while True:
    type_choose = input("Будь ласка, оберіть тип умовної конструкції (від 1 до 3): ")  # вибір умовної конструкції
    if type_choose == str(1):
        type1()
        break
    elif type_choose == str(2):
        type2()
        break
    elif type_choose == str(3):
        type3()
        break
    else: 
        print("Некоректна відповідь")
        continue
