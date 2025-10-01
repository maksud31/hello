from numbers import Real
from typing import Optional, List, Union


def calculate_average(numbers: List[Union[int, float]]) -> Optional[float]:
    """Вычисляет среднее арифметическое значение списка чисел."""
    
    Args:
        numbers: Список чисел (int или float) для вычисления среднего
        
    Returns:
        Optional[float]: Среднее значение или None если список пуст
        
    Examples:
        >>> calculate_average([10, 20, 30, 40])
        25.0
        >>> calculate_average([])
        None
        
    Note:
        Для пустого списка возвращает None вместо исключения
    """
    # Проверка на пустой список
    if not numbers:
        return None
    
    # Вычисление среднего значения
    total = sum(numbers)
    average = total / len(numbers)
    
    return average


def calculate_average_safe(numbers: List[Union[int, float]]) -> float:
    """Безопасная версия вычисления среднего с обработкой исключений.
    
    Args:
        numbers: Список чисел для вычисления среднего
        
    Returns:
        float: Среднее значение
        
    Raises:
        ValueError: Если список пустой или содержит нечисловые значения
        
    Examples:
        >>> calculate_average_safe([1, 2, 3])
        2.0
        >>> calculate_average_safe([])
        ValueError: Cannot calculate average of empty list
    """
    if not numbers:
        raise ValueError("Cannot calculate average of empty list")
    
    # Проверка типов элементов
    for i, num in enumerate(numbers):
        if not isinstance(num, Real):
            raise TypeError(f"Element at index {i} is not a number: {num}")
    
    return sum(numbers) / len(numbers)


def calculate_statistics(numbers: List[Union[int, float]]) -> dict:
    """Вычисляет расширенную статистику для набора чисел.
    
    Args:
        numbers: Список чисел для анализа
        
    Returns:
        dict: Словарь с различными статистическими показателями
        
    Examples:
        >>> stats = calculate_statistics([10, 20, 30, 40])
        >>> stats['average']
        25.0
    """
    if not numbers:
        return {
            'average': None,
            'min': None,
            'max': None,
            'count': 0,
            'total': 0
        }
    
    return {
        'average': calculate_average(numbers),
        'min': min(numbers),
        'max': max(numbers),
        'count': len(numbers),
        'total': sum(numbers)
    }


class StatisticsCalculator:
    """Класс для работы со статистическими вычислениями.
    
    Attributes:
        data (List[float]): Набор данных для анализа
    """
    
    def __init__(self, data: Optional[List[Union[int, float]]] = None):
        """Инициализация калькулятора статистики.
        
        Args:
            data: Начальный набор данных (опционально)
        """
        self.data = list(data) if data is not None else []
    
    def add_number(self, number: Union[int, float]) -> None:
        """Добавляет число в набор данных.
        
        Args:
            number: Число для добавления
        """
        if not isinstance(number, Real):
            raise TypeError("Can only add numbers to statistics data")
        self.data.append(float(number))
    
    def calculate_average(self) -> Optional[float]:
        """Вычисляет среднее значение текущего набора данных."""
        return calculate_average(self.data)
    
    def clear_data(self) -> None:
        """Очищает набор данных."""
        self.data.clear()
    
    def get_summary(self) -> dict:
        """Возвращает сводную статистику по данным."""
        return calculate_statistics(self.data)


# Примеры использования и тестирование
def demonstrate_usage():
    """Демонстрация использования рефакторированного кода."""
    print("=== Демонстрация работы рефакторированного кода ===\n")
    
    # Пример 1: Базовая функция
    numbers_list = [10, 20, 30, 40]
    result = calculate_average(numbers_list)
    
    print("1. Базовая функция:")
    print(f"   Данные: {numbers_list}")
    if result is not None:
        print(f"   Среднее значение: {result:.2f}")
    else:
        print("   Список пуст")
    
    # Пример 2: Обработка пустого списка
    empty_list = []
    empty_result = calculate_average(empty_list)
    print(f"\n2. Пустой список: {empty_list}")
    print(f"   Результат: {empty_result}")
    
    # Пример 3: Расширенная статистика
    print("\n3. Расширенная статистика:")
    stats = calculate_statistics(numbers_list)
    for key, value in stats.items():
        print(f"   {key}: {value}")
    
    # Пример 4: Использование класса
    print("\n4. Использование класса StatisticsCalculator:")
    calculator = StatisticsCalculator(numbers_list)
    print(f"   Среднее: {calculator.calculate_average():.2f}")
    
    # Добавляем новое число
    calculator.add_number(50)
    print(f"   После добавления 50: {calculator.calculate_average():.2f}")
    
    # Пример 5: Безопасная версия с исключениями
    print("\n5. Безопасная версия:")
    try:
        safe_result = calculate_average_safe(numbers_list)
        print(f"   Результат: {safe_result:.2f}")
        
        # Это вызовет исключение
        calculate_average_safe([])
    except ValueError as e:
        print(f"   Ошибка: {e}")


def run_tests():
    """Запуск тестов для проверки корректности."""
    print("\n=== Тестирование функций ===")
    test_cases = [
        ([1, 2, 3, 4, 5], 3.0),
        ([10], 10.0),
        ([], None),
        ([0, 0, 0], 0.0),
    ]
    for i, (numbers, expected) in enumerate(test_cases, 1):
        result = calculate_average(numbers)
        status = "✓" if result == expected else "✗"
        print(f"Тест {i}: {numbers} -> {result} {status}")
if __name__ == "__main__":
    demonstrate_usage()
