    Лабораторна робота №6    

Автор:Коломійченко Богдан Сергійович
Група:ІПЗ-13
Варіант:7

                            Завдання

7.	У рядку слів визначити кількість слів і надрукувати ті, довжина яких більша за вказану користувачем. Якщо слово починається із заданого користувачем символу, то замінити його на перше слово у рядку.

string = input("Наберіть речення: ")
while True:
    try:
        min_len = int(input("Мінімальна кількість букв в слові: "))
        break
    except ValueError:
        print("Невірне значення. Спробуйте знову.")
symbol = input("Оберіть символ: ")  # задання значень для обробки
symbol_ignore = ""
while True:
    ignore_caps = input("Ігнорувати CAPS LOCK? (1 - так / 0 - ні): ")  # опціональна можливість ігнорувати велику літеру
    if ignore_caps == "0":
        break
    elif ignore_caps == "1":
        if symbol.isupper():
            symbol_ignore = symbol.lower()
        elif symbol.islower():
            symbol_ignore = symbol.upper()
        break
    print("Некорректне значення!")  # безкінечний запит із захистом від помилок
split_string = string.split()
print("Кількість слів в рядку: " + str(len(split_string)))  # суммарна кількість слів в рядку
counter = 0
for i in range(len(split_string)):  # цикл для виведення слів з рядка що відповідають вимозі
    if len(string.split()[i]) > min_len:
        print(" -> " + string.split()[i])
        counter += 1
print("Кількість слів за вимогою: " + str(counter), end="\n\n")

print("Результуюче речення після заміни слів (спрацює лише у випадку співпадіння обраного символа)")
for i in range(len(split_string)):  # аналіз співпадіння першого символу у слові з урахуванням опції ігнорування
    if ignore_caps == "0":  # при ігнорування = вимкнено
        if split_string[i][0] == symbol:
            split_string[i] = split_string[0]
    elif ignore_caps == "1":  # при ігнорування = ввімкнено
        if split_string[i][0] == symbol or split_string[i][0] == symbol_ignore:
            split_string[i] = split_string[0]
for i in range(len(split_string)):
    print(split_string[i], end=" ")
