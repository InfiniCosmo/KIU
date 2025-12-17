int, input, print, if, else, elif, print, sep, end, //, /, *, >, <, =, lower. random




import random

def get_valid_answer(question, options):
    while True:
        print(question)
        for i, option in enumerate(options, 1):
            print(f"{i}. {option}")
        try:
            answer = input("Ваш ответ (1-3): ").strip()
            if answer in ["1", "2", "3"]:
                return answer
            else:
                print("Пожалуйста, введите число от 1 до 3.")
        except KeyboardInterrupt:
            print("\nПрограмма прервана пользователем.")
            exit()

def get_random_bonus(bonuses):
    return random.choice(bonuses)

def save_result(filename, content):
    try:
        with open(filename, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Результат успешно сохранён в файл '{filename}'.")
    except PermissionError:
        print("Ошибка: нет прав на запись в файл.")
    except FileNotFoundError:
        print("Ошибка: не удалось найти путь к файлу.")
    except Exception as e:
        print(f"Произошла ошибка при сохранении файла: {e}")

def main():
    print("Добро пожаловать в магический тест на личность!")
    print("Ответьте на 3 вопроса, чтобы узнать свою магическую сущность.")
    print("Для ответа введите число от 1 до 3 и нажмите Enter.\n")

    questions = [
        ("Какой элемент природы вам ближе?", ["Огонь", "Вода", "Земля"]),
        ("Какое животное вас вдохновляет?", ["Дракон", "Феникс", "Единорог"]),
        ("Что вы выберете в бою?", ["Магический посох", "Заклинание иллюзии", "Защитный амулет"])
    ]

    wizard_points = 0
    elf_points = 0
    dwarf_points = 0

    q1 = get_valid_answer(questions[0][0], questions[0][1])
    q2 = get_valid_answer(questions[1][0], questions[1][1])
    q3 = get_valid_answer(questions[2][0], questions[2][1])

    if q1 == "1": wizard_points += 2; elf_points += 1
    elif q1 == "2": elf_points += 2; dwarf_points += 1
    elif q1 == "3": dwarf_points += 2; wizard_points += 1

    if q2 == "1": wizard_points += 2; dwarf_points += 1
    elif q2 == "2": elf_points += 2; wizard_points += 1
    elif q2 == "3": dwarf_points += 2; elf_points += 1

    if q3 == "1": wizard_points += 3
    elif q3 == "2": elf_points += 3
    elif q3 == "3": dwarf_points += 3

    max_points = max(wizard_points, elf_points, dwarf_points)
    if wizard_points == max_points:
        entity = "Волшебник"
        description = "Вы обладаете великой магической силой и мудростью. Ваши заклинания способны изменить мир!"
    elif elf_points == max_points:
        entity = "Эльф"
        description = "Вы легки и грациозны, связаны с природой и обладаете острым умом. Ваша магия — это гармония и красота."
    else:
        entity = "Гном"
        description = "Вы крепки духом и телом, мастерски владеете древними артефактами. Ваша сила — в упорстве и мастерстве."

    total_points = wizard_points + elf_points + dwarf_points
    magic_level = min((total_points // 3) + 1, 10)

    bonuses = [
        "Магический амулет защиты",
        "Свиток древних заклинаний",
        "Кристалл жизненной энергии",
        "Перстень невидимости",
        "Зелье силы"
    ]
    bonus = get_random_bonus(bonuses)

    print("\n" + "="*50)
    print("РЕЗУЛЬТАТ МАГИЧЕСКОГО ТЕСТА")
    print("="*50)
    print(f"Ваша магическая сущность: {entity}")
    print(f"Описание: {description}")
    print(f"Уровень магии: {magic_level}/10")
    print(f"Ваш магический бонус: {bonus}")
    print("="*50)

    save_choice = input("\nХотите сохранить результат в файл? (да/нет): ").strip().lower()
    if save_choice in ["да", "yes", "y"]:
        filename = "magic_test_result.txt"
        content = (
            f"РЕЗУЛЬТАТ МАГИЧЕСКОГО ТЕСТА\n"
            f"Сущность: {entity}\n"
            f"Описание: {description}\n"
            f"Уровень магии: {magic_level}/10\n"
            f"Бонус: {bonus}\n"
            f"Ответы: {q1}, {q2}, {q3}\n"
        )
        save_result(filename, content)

    print("Спасибо за прохождение магического теста! Да пребудет с вами магия!")

if __name__ == "__main__":
    main()
