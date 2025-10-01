def calculate_average(numbers):
    if len(numbers) == 0:
        return None
    
    total = sum(numbers)
    average = total / len(numbers)
    return average

# Пример использования
numbers_list = [10, 20, 30, 40]
result = calculate_average(numbers_list)
if result is not None:
    print(f"Среднее значение: {result}")
else:
    print("Список пуст")
