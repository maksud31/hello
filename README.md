from numbers import Real
from typing import Optional, List, Union


def calculate_average(numbers: List[Union[int, float]]) -> Optional[float]:
    """Вычисляет среднее арифметическое значение списка чисел."""
    
    Args:
        numbers: Список чисел (int или float) для вычисления среднегоо
        
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
