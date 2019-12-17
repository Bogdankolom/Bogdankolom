                  Лабораторна робота №9   

Автор: Коломійченко Богдан Сергійович
Група:ІПЗ-13
Варіант:7

9.	Скласти програму для обробки текстового та бінарного файлів. Передбачити меню вибору задач 
a.	Створити текстовий файл F. Увести з клавіатури рядок символів S. Отримати всі рядки файлу F, що містять у собі підрядок S і записати їх до нового файлу G. Останнім рядком файлу G записати кількість знайдених у файлі F рядків.
b.	У програму лабораторної роботи №8 додати нові функції обробки бінарних файлів:
–	створений у лабораторній роботі №8 словник записати до бінарного файлу;
–	надрукувати словник у вигляді таблиці, зчитавши дані з бінарного файлу;
–	розробити функції, які реалізують операції додавання у бінарний файл нових даних, видалення даних за запитом користувача, заміни одних значень іншими на вимогу користувача;
–	результати запитів, які реалізовані в лабораторній роботі №8, записати до бінарного файлу і вивести на екран

task1_dict = {}
entry_value = []
entry_in_progress = True
hint_counter = 1
entry_in_progress_counter = 0
currency_rate = 0


def task1_entry():
    global entry_counter
    global entry_value
    global entry_in_progress
    global entry_in_progress_counter
    global hint_counter
    global currency_rate
    if entry_in_progress_counter == 0:
        print("Для того щоб зупинити введення введіть - . - як символ")
        entry_in_progress_counter = 1
    entry_hint = [str(hint_counter) + ". Назва фірми: ", str(hint_counter) + ". Назва продукту: ",
                  str(hint_counter) + ". Ціна в доларах: "]
    for entry_counter in range(0, 3):
        entry_value.insert(entry_counter, input(entry_hint[entry_counter]))
        if entry_value[entry_counter] == ".":
            print("")
            hint_counter -= 1
            entry_in_progress = False
            break
    if entry_value != ['.']:
        entry_value.append(str(float(entry_value[2]) * float(currency_rate)) + "₴")
    hint_counter += 1
    if entry_value[entry_counter] != ".":
        dictlength = len(task1_dict) + 1
        task1_dict.update({dictlength: entry_value})
    entry_value = []


def call_task1_dict():
    global task1_dict
    for a in range(1, len(task1_dict) + 1):
        print(str(a) + ": " + task1_dict[a][0] + ". " + task1_dict[a][1] + ", " + task1_dict[a][2] + "$" + ", "
              + task1_dict[a][3] + "₴")


def task1():
    global entry_in_progress
    global task1_dict
    global entry_value
    global currency_rate
    first_call_done = False
    print("Завдання з фірмами, продуктами і цінами")
    print("Доступне виведення результатів роботи в файл. За запитом і при завершенні програми")
    currency_rate = input("Введіть курс гривні до доллара. Рекомендоавно едине значення НБУ: ")
    while True:
        while entry_in_progress:
            task1_entry()
        if not first_call_done:
            call_task1_dict()
            first_call_done = True
        print("")
        print("1 - викликати весь список")
        print("2 - редагувати запис")
        print("3 - додати ще один запис")
        print("4 - вивести результати в файл")
        print("0 - повернутися до головного меню")
        task1_menu = input("Вибір?: ")
        if task1_menu == "1":
            call_task1_dict()
        elif task1_menu == "2":
            if not first_call_done:
                call_task1_dict()
            chosen_entry = int(input("Оберіть запис для редагування: "))
            print(str(chosen_entry) + ": " + task1_dict[chosen_entry][0] + ". " + task1_dict[chosen_entry][1] +
                  ", " + task1_dict[chosen_entry][2])
            entry_hint = [str(chosen_entry) + ". Назва фірми: ", str(chosen_entry) + ". Назва продукту: ",
                          str(chosen_entry) + ". Ціна в доларах: "]
            print("Натискайте ENTER без додаткового введення якщо хочете залишити значення без змін")
            for edit_counter in range(0, 3):
                entry_value.insert(edit_counter, input(entry_hint[edit_counter]))
                if entry_value[edit_counter] == "":
                    entry_value[edit_counter] = task1_dict[chosen_entry][edit_counter]
            entry_value.insert(3, str(float(entry_value[2]) * float(currency_rate)) + "₴")
            task1_dict.update({chosen_entry: entry_value})
            chosen_entry = 0
            edit_counter = 0
            entry_value = []
        elif task1_menu == "3":
            task1_entry()
        elif task1_menu == "4":
            pass
        elif task1_menu == "0":
            break
        else:
            print("Помилка. Введено невідоме значення.")
            continue


print("ІПЗ-13, Коломійченко Богдан Сергійович")
print("Лабораторна робота 9")
print("Варіант 7")

print("Меню")
print("1 - робота з текстовим файлом і цінами")
print("0 - вихід з програми")
while True:
    menu = input("Вибір завдання?: ")
    if menu == "1":
        task1()
    elif menu == "0":
        exit(0)
    else:
        print("Некорректна відповідь. Спробуйте ще раз.")
        continue
