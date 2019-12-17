                      Лабораторна робота №8     

Автор: Коломійченко Богдан Сергійович
Група:ІПЗ-13
Варіант:7

8.	Скласти програму для обробки словнику та множини. Передбачити меню вибору задач 
a.	Створити словник, який має декілька ключів та значень. Кожному ключу відповідає масив таких елементів: прізвище викладача, назва дисципліни, кількість навчальних годин з дисципліни, кількість студентів на потоці, які вивчають дисципліну. Надрукувати словник. Реалізувати такі запити: 1) визначити викладачів, які викладають задану з клавіатури дисципліну; 2) визначити дисципліну, яку вивчає найбільша кількість студентів; 3) визначити сумарну кількість навчальних годин з усіх дисциплін, які записані у словнику.
b.	Задано текст з латинських літер. Символи цього тексту формують множину. Скласти програму, яка визначає і виводить на екран: а) перші входження літер в текст, зберігаючи їх вихідний взаємний порядок; б) всі літери, які входять в текст не менше двох разів; в) всі літери, які входять в текст один раз.

task1_dict = {}
entry_value = []
entry_in_progress = True
entry_in_progress_counter = 0
hint_counter = 1
first_call_done = False


def task1_entry(): 

    global entry_counter
    global entry_value
    global entry_in_progress
    global entry_in_progress_counter
    global hint_counter
    if entry_in_progress_counter == 0:
        print("Для того щоб зупинити введення введіть - . - як символ")
        entry_in_progress_counter = 1
    entry_hint = [str(hint_counter) + ". Назва книги: ", str(hint_counter) + ". Прізвище автора: ",
                  str(hint_counter) + ". Рік видання: "]
    for entry_counter in range(0, 3):  # перебирання значень з допомогою циклу і підставленнням підказок з масиву
        entry_value.insert(entry_counter, input(entry_hint[entry_counter]))
        if entry_value[entry_counter] == ".":  # зупинка введення з виконанням сервісних операцій
            print("")
            hint_counter -= 1
            entry_in_progress = False
            break
    hint_counter += 1
    if entry_value[entry_counter] != ".":  # додавання отриманих значень до словника
        dictlength = len(task1_dict) + 1
        task1_dict.update({dictlength: entry_value})
    entry_value = []  # обнулення масиву для можливості коректного повторного виклику


def task1_call():  # функція для виведення поточного стану словника першого завдання
    global task1_dict
    for a in range(1, len(task1_dict) + 1):
        print(str(a) + ": " + task1_dict[a][0] + ". " + task1_dict[a][1] + ", " + task1_dict[a][2])


def task1_search_by_year():  # функція пошуку за роком видання
    global task1_dict
    search_year = input("Оберіть рік видання: ")
    for b in range(1, len(task1_dict) + 1):
        if search_year == task1_dict[b][2]:
            print(str(b) + ": " + task1_dict[b][0] + ". " + task1_dict[b][1])


def task1_search_by_author():  # функція пошуку за автором
    global task1_dict
    search_author = input("Оберіть автора: ")
    for c in range(1, len(task1_dict) + 1):
        if search_author == task1_dict[c][1]:
            print(str(c) + ": " + task1_dict[c][0] + ". " + task1_dict[c][2])


def task1_edit():  # функція редагування записів
    global first_call_done
    global entry_value
    global task1_dict
    if not first_call_done:
        task1_call()
    chosen_entry = int(input("Оберіть запис для редагування: "))
    print(str(chosen_entry) + ": " + task1_dict[chosen_entry][0] + ". " + task1_dict[chosen_entry][1] +
          ", " + task1_dict[chosen_entry][2])
    entry_hint = [str(chosen_entry) + ". Назва книги: ", str(chosen_entry) + ". Прізвище автора: ",
                  str(chosen_entry) + ". Рік видання: "]
    print("Натискайте ENTER без додаткового введення якщо хочете залишити значення без змін")
    for edit_counter in range(0, 3):
        entry_value.insert(edit_counter, input(entry_hint[edit_counter]))
        if entry_value[edit_counter] == "":  # збереження без змін при пропуску введення
            entry_value[edit_counter] = task1_dict[chosen_entry][edit_counter]
    task1_dict.update({chosen_entry: entry_value})  # повернення відредагованих значень в словник
    del chosen_entry
    del edit_counter
    entry_value = []  # обнулення змінних для подальшої корректної роботи


def task1_delete():  # функція видалення записів
    global hint_counter
    global task1_dict
    if not first_call_done:
        task1_call()
    delete_entry = int(input("Оберіть запис для видалення: "))
    if delete_entry in task1_dict:
        print(str(delete_entry) + ": " + task1_dict[delete_entry][0] + ". " + task1_dict[delete_entry][1] +
              ", " + task1_dict[delete_entry][2], end="\n\n")
        print("Підтвердьте видалення запису")
        confirm_delete = input("Введіть del" + str(delete_entry) + ": ")  # захист від випадкового видалення
        if confirm_delete == "del" + str(delete_entry):
            task1_dict.pop(delete_entry)
            hint_counter -= 1
            for resort_entry in range(delete_entry, len(task1_dict) + 1):
                # переміщення записів на одну позицію при видаленні з середини або з початку
                task1_dict.update({resort_entry: task1_dict.get(resort_entry + 1)})
            if not delete_entry > len(task1_dict):
                # при видаленні з середини або з початку з'являеться дублікат, ця інструкція не повинна
                # виконуватися для видалень з кінця
                task1_dict.pop(len(task1_dict))
            task1_call()
        else:
            print("Видалення зупинено!")


def task1():  # Функція основного керування першим завданням
    global entry_in_progress
    global task1_dict
    global entry_value
    global hint_counter  # робота з глобальними змінними
    global first_call_done
    print("Завдання з авторами книг")
    while True:
        while entry_in_progress:  # керування режимом введення після першого запуску програми
            task1_entry()
        if not first_call_done:  # виведення результатів введення після першого запуску програми
            task1_call()
            first_call_done = True
        print("")
        print("1 - викликати весь список")
        print("2 - книги за роком видання")
        print("3 - книги за авторами")
        print("4 - упорядкувати за прізвищем автора (не створено)")
        print("5 - редагувати запис")
        print("6 - додати ще один запис")
        print("7 - видалити запис")
        print("0 - повернутися до головного меню")  # меню доступних операцій
        task1_menu = input("Вибір?: ")
        if task1_menu == "1":  # викликати весь список
            task1_call()
        elif task1_menu == "2":  # пошук за роком видання
            task1_search_by_year()
        elif task1_menu == "3":  # пошук за автором
            task1_search_by_author()
        elif task1_menu == "4":  # упорядкувати за прізвищем автора
            print("Нажаль функція все ще в розробці...")
        elif task1_menu == "5":  # редагування записів
            task1_edit()
        elif task1_menu == "6":  # додавання нових записів
            task1_entry()
        elif task1_menu == "7":  # видалення записів
            task1_delete()
        elif task1_menu == "0":  # вихід з програми
            break
        else:
            print("Помилка. Введено невідоме значення.")
            continue


def task2():  # Функція основного керування другим завданням
    letters = {"a": 0, "e": 0, "i": 0, "o": 0, "u": 0, "y": 0}
    numeral = {"1": 0, "2": 0, "3": 0, "4": 0, "5": 0, "6": 0, "7": 0, "8": 0, "9": 0, "0": 0}
    letters_service = "aeiouy"
    numeral_service = "1234567890"  # сервісні змінні які працюють як ключі для словника при переборі значень
    while True:
        task2_entry = input("Введіть рядок який складається з цифр і англійських букв: ")
        for d in range(len(task2_entry)):
            for e in range(len(letters_service)):  # додавати одиницю до літери в переборі при її знаходженні
                if task2_entry[d] == letters_service[e]:
                    letters.update({letters_service[e]: letters.get(letters_service[e]) + 1})
            for f in range(len(numeral_service)):  # додавати одиницю до цифри в переборі при її знаходженні
                if task2_entry[d] == numeral_service[f]:
                    numeral.update({numeral_service[f]: numeral.get(numeral_service[f]) + 1})
        letters_header = '%20s' % "Англійські голосні: "  # виведення результатів
        print(letters_header, end="")
        for h in range(len(letters_service) - 1):
            print(str(letters_service[h]) + ": " + str(letters.get(letters_service[h])), end=", ")
        print(str(letters_service[h + 1]) + ": " + str(letters.get(letters_service[h + 1])))
        numeral_header = '%20s' % "Цифри: "
        print(numeral_header, end="")
        for i in range(len(numeral_service) - 1):
            print(str(numeral_service[i]) + ": " + str(numeral.get(numeral_service[i])), end=", ")
        print(str(numeral_service[i + 1]) + ": " + str(numeral.get(numeral_service[i + 1])))
        break


print("ІПЗ-13, Коломійченко Богдан Сергійович")
print("Лабораторна робота 8")
print("Варіант 7")

while True:
    print("Меню вибору задач")
    print("1 - словники з інформацією про книги")
    print("2 - введення рядка і визнчення множин")
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
