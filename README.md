from typing import Optional, List, Union


def calculate_average(numbers: List[Union[int, float]]) -> Optional[float]:
    """
    Вычисляет среднее арифметическое значение списка чисел.
    
    Args:
        numbers: Список чисел (целых или вещественных)
        
    Returns:
        Среднее значение или None, если список пуст
    """
    # Проверка на пустой список
    if not numbers:
        return None
    
    # Проверка, что все элементы являются числами
    if not all(isinstance(num, (int, float)) for num in numbers):
        raise ValueError("Все элементы списка должны быть числами")
    
    try:
        total = sum(numbers)
        average = total / len(numbers)
        return average
    except ZeroDivisionError:
        # Эта ошибка не должна возникать из-за проверки выше, но для безопасности оставлю
        return None


def format_average_result(average: Optional[float]) -> str:
    """
    Форматирует результат вычисления среднего значения для вывода.
    
    Args:
        average: Рассчитанное среднее значение или None
        
    Returns:
        Отформатированная строка для вывода
    """
    if average is None:
        return "Список пуст"
    else:
        return f"Среднее значение: {average:.2f}"


def main():
    """Основная функция для демонстрации работы."""
    # Тестовые данные
    test_cases = [
        [10, 20, 30, 40],  # нормальный случай
        [],                 # пустой список
        [5.5, 10.2, 15.8], # вещественные числа
        [42],               # один элемент
    ]
    
    for i, numbers_list in enumerate(test_cases, 1):
        print(f"Тест {i}: {numbers_list}")
        
        try:
            result = calculate_average(numbers_list)
            output = format_average_result(result)
            print(output)
        except ValueError as e:
            print(f"Ошибка: {e}")
        
        print("-" * 30)


# Пример использования (сохранен для обратной совместимости)
if __name__ == "__main__":
    # Оригинальный пример использования
    numbers_list = [10, 20, 30, 40]
    result = calculate_average(numbers_list)
    
    if result is not None:
        print(f"Среднее значение: {result}")
    else:
        print("Список пуст")
    
    print("\n" + "="*50 + "\n")
    
    # Запуск расширенного тестирования
    main()
