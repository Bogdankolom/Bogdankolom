    Лабораторна робота №7     

Автор:Коломійченко Богдан Сергійович
Група:ІПЗ-13
Варіант:7

7.	Скласти програму для обробки одновимірного масиву та матриці. Передбачити меню вибору задач 
a.	У згенерованому числовому списку знайти найбільший серед від’ємних та найменший серед додатних елементів списку. Вивести список, значення знайдених елементів та їх індекси.
b.	В кінотеатрі n рядів по m місць в кожному. У двовимірному масиві зберігається інформація про продані квитки: число 1 означає, що квиток на дане місце вже проданий, число 0 означає, що місце вільне. Надійшов запит на продаж k квитків на сусідні місця в одному ряду. Визначте, чи можна виконати такий запит. 

import random

# Імпорт бібліотеки, оголошення глобальних змінних та массивів
task1_auto_list, task1_auto_negative, task1_auto_positive, task1_manual_list, task1_manual_negative, \
    task1_manual_positive, task2_list = [], [], [], [], [], [], []
# Python Enhancement Proposal 8, стиль коду заданий розробниками мови - строка < 120 символів для зручності читання
rows, seats = 0, 0
# Розбиття массиву зі значеннями на негативний і позитивний зі збереженням індексів
# Функція створена з використанням передачі змінних для використання одразу в автоматичному і ручному режимі


def task1_prep(list_in_processing, list_for_positive, list_for_negative):
    for a in range(len(list_in_processing)):
        if int(list_in_processing[a]) > 0:
            list_for_positive.insert(a, "")
            list_for_negative.insert(a, int(list_in_processing[a]))
        elif int(list_in_processing[a]) < 0:
            list_for_negative.insert(a, "")
            list_for_positive.insert(a, int(list_in_processing[a]))
    task1_evaluator(list_in_processing, list_for_positive, list_for_negative)


# Забиття пустих елементів массивів для корректної роботи функцій аналізу


def task1_evaluator(processed, negative, positive):
    print(processed)
    for b in range(0, len(negative)):
        if negative[b] == '':
            negative[b] = -999999999999999999999999999999999999999999999999999999999999999999
        negative[b] = int(negative[b])
    for c in range(0, len(positive)):
        if positive[c] == '':
            positive[c] = 999999999999999999999999999999999999999999999999999999999999999999
        positive[c] = int(positive[c])
    if max(negative) == -999999999999999999999999999999999999999999999999999999999999999999:
        print("Не було введено від'ємних чисел")
    else:
        print("Найбільше від'ємне число є елементом №" + str(negative.index(max(negative)) + 1) + ": " +
              str(max(negative)))
    # Python Enhancement Proposal 8, стиль коду заданий розробниками мови - строка < 120 символів для зручності читання
    if min(positive) == 999999999999999999999999999999999999999999999999999999999999999999:
        print("Не було введено додатних чисел")
    else:
        print("Найменше додатнє число є елементом №" + str(positive.index(min(positive)) + 1) + ": " +
              str(min(positive)))
    # Python Enhancement Proposal 8, стиль коду заданий розробниками мови - строка < 120 символів для зручності читання


def task1():  # Функція основного керування першим завданням
    global task1_auto_list, task1_auto_negative, task1_auto_positive, task1_manual_list, task1_manual_negative, \
           task1_manual_positive, task1_auto_length
    # Python Enhancement Proposal 8, стиль коду заданий розробниками мови - строка < 120 символів для зручності читання
    # Перехід на керування змінними на глобальному рівні програми
    print("Найбільше від'ємне і найменше додатнє")
    print("Згенерувати список автоматично чи ввести вручну?")
    print("1 - автоматично / 0 - вручну")
    while True:  # Бескінечний цикл меню
        task1_menu = input("Вибір?: ")
        if task1_menu == "1":
            print("Розмір списку повинен бути не менше ніж 4 елементи для гарного порівняння")
            while True:
                print("Автоматичний режим")  # Автоматичний режим із захистом від нечислового введення
                try:
                    task1_auto_length = int(input("Розмір списку: "))
                except ValueError:
                    print("Помилка. Введено не числове значення.")
                    continue
                if task1_auto_length >= 4:
                    break
                print("Занадто малий список")
            for d in range(0, task1_auto_length):  # Частина яка відповідає за генерацію випадкових чисел
                task1_auto_list.append(random.randrange(-32768, 32767))  # За радіус генерації взято обмедення С++
            task1_prep(task1_auto_list, task1_auto_positive, task1_auto_negative)
            # Перекидання на функцію розбиття масивів
            break
        elif task1_menu == "0":
            print("Ручний режим")
            print("Введіть крапку як символ - . - для того щоб зупинити введення")
            manual_list_entry_mode = True
            while manual_list_entry_mode:  # Ручний режим який зупиняється введенням точки
                manual_list_entry = input("Нове значення: ")
                if manual_list_entry == "." and len(task1_manual_list) != 0:
                    manual_list_entry_mode = False  # Вихід з циклу при знаходженні точки
                    continue
                else:
                    try:  # Спроба дописання значення до масиву з захистом від нечислових значень
                        task1_manual_list.append(int(manual_list_entry))
                    except ValueError:
                        if manual_list_entry == ".":
                            print("Помилка. Пустий список.")  # Захист від помилки пустого списку
                        else:
                            print("Помилка. Введено не числове значення.")
                        continue
                    print("Вже введено значень: " + str(len(task1_manual_list)))
            task1_prep(task1_manual_list, task1_manual_positive, task1_manual_negative)
            # Перекидання на функцію розбиття масивів
        else:
            print("Помилка. Введено невідоме значення.")
            continue  # Викидання на вибір ручного/автоматичного режиму якщо введено невірне значення
        break
    task1_auto_list, task1_auto_negative, task1_auto_positive, task1_manual_list, task1_manual_negative, \
        task1_manual_positive = [], [], [], [], [], []
    # Очищення масивів для того щоб можна було викликати функцію знову без помилок


def task2():  # Функція основного керування другим завданням
    seats_counter = 0
    found = []  # Оголошення локальних змінних які не потребують роботи на глобальному рівні
    global task2_list, seats_requested, rows, seats
    print("Задача з кінотеатром")
    while True:  # Бескінечний цикл меню
        print("Обрати кількість місць: 1 - автоматично / 0 - вручну")
        while True:
            task2_menu = input("Режим задання місць?: ")
            if task2_menu == "1":
                print("Автоматичний режим")
                rows = random.randrange(5, 30)  # Частина яка відповідає за випадковий вибір "розміру кінотеатру"
                seats = rows * 2
            elif task2_menu == "0":
                print("Ручний режим")
                try:
                    rows = int(input("Кількість рядків: "))  # Ручне задання "розміру кінотеатру"
                    seats = int(input("Кількість місць в рядку: "))
                except ValueError:
                    print("Нечислове значення!")
                    continue
            else:
                print("Помилка. Введено невідоме значення.")
                continue  # Захист від некорректних значень
            break
        temp_list = []  # Початок частини випадкового вибору "проданих місць"
        for e in range(0, rows):
            temp_list.append([])
            for f in range(0, seats):
                temp_list[e].insert(f, random.randrange(0, 2))
            task2_list.insert(e, temp_list[e])  # Кінець частини випадкового вибору "проданих місць"
        print("ЕКРАН".center(seats + 2 * (seats - 1)))  # Початок частини що відповідає за заголовок зі "стовпчиками"
        counter_var = 0
        header = '%5s' % ("N" + ": ")
        print(header, end="")
        for g in range(0, seats - 1):
            header_counter = '%2s' % (str(g + 1))
            print(header_counter, end=" ")
            counter_var += 1
        print(counter_var + 1)  # Кінець частини що відповідає за заголовок зі "стовпчиками"
        for h in range(0, len(task2_list)):
            # Початок частини що відповідає за вивід рядків, з вказанням знчень "продано?"
            export = '%5s' % (str(h + 1) + ": ")
            print(export, end="")
            print(task2_list[h])  # Кінець частини що відповідає за вивід рядків, з вказанням знчень "продано?"
        break
    while True:  # Захищений від помилок запит щодо шуканої кількості місць для придбання
        try:
            seats_requested = int(input("Кількість місць для продажу?: "))
        except ValueError:
            print("Помилка. Введено не числове значення.")
            continue
        break
    for i in range(0, rows):
        # Початок частини яка відповідає за перебір массивів в пошуках повторень числа 0 задану кілкість разів
        for j in range(0, seats):
            if task2_list[i][j] == 0:
                seats_counter += 1
            if seats_counter == seats_requested:
                found.append(i + 1)
                seats_counter = 0
            if task2_list[i][j] != 0:
                seats_counter = 0
    for k in range(0, len(found)):
        print("Доступний ряд: " + str(found[k]))
        # Кінець частини яка відповідає за перебір массивів в пошуках повторень числа 0 задану кілкість разів
    task2_list = []
    rows, seats = 0, 0  # Очищення масивів для того щоб можна було викликати функцію знову без помилок


print("ІПЗ-13, Коломійченко Богдан Сергійович")
print("Лабораторна робота 7")
print("Варіант 7")


# Інформаційна частина, виведення авторства, безкінечний цикл меню
while True:
    print("Меню вибору задач")
    print("1 - задача з найменшим додатним і найбільшим від'ємним")
    print("2 - задача з місцями в кінотеатрі")
    print("0 - вихід з програми")
    menu = input("Вибір завдання?: ")
    if menu == "1":
        task1()
    elif menu == "2":
        task2()
    elif menu == "0":
        exit(0)
    else:
        print("Некорректна відповідь. Спробуйте ще раз.")
        continue
