# Лабораторная работа №16: Планировщик задач на Python

## Цель работы
Целью данной лабораторной работы является реализация и проверка работы планировщика задач на языке Python, который позволяет добавлять, удалять, обновлять и управлять задачами.

## Описание задания
Реализовать класс `Task` для представления задачи и класс `Schedule` для управления списком задач.

## Описание классов

### Класс `Task`
Класс `Task` представляет одну задачу со следующими атрибутами:
- `title`: Заголовок задачи.
- `description`: Описание задачи.
- `due_date`: Дата выполнения задачи.
- `status`: Статус задачи (по умолчанию "Pending").
- `priority`: Приоритет задачи (по умолчанию "Medium").
- `notes`: Дополнительные заметки.
- `duration`: Продолжительность задачи в часах.
- `recurrence`: Периодичность задачи (например, "еженедельно").

### Класс `Schedule`
Класс `Schedule` управляет списком задач и поддерживает следующие методы:
- `add_task(task)`: Добавляет задачу в список задач.
- `remove_task(task_title)`: Удаляет задачу из списка задач по ее заголовку.
- `get_task(task_title)`: Возвращает задачу по ее заголовку.
- `list_overdue_tasks()`: Возвращает список просроченных задач.
- `list_tasks_due_today()`: Возвращает список задач, которые должны быть выполнены сегодня.
- `sort_tasks_by_due_date()`: Возвращает список задач, отсортированный по дате выполнения.
- `update_task(task_title, **kwargs)`: Обновляет атрибуты задачи.
- `mark_as_completed(task_title)`: Отмечает задачу как выполненную.
- `list_completed_tasks()`: Возвращает список выполненных задач.
- `find_task_by_keyword(keyword)`: Ищет задачи по ключевому слову в заголовке или описании.
- `check_deadlines()`: Проверяет задачи с дедлайном на завтра.
- `list_all_tasks()`: Возвращает список всех задач.
- `list_tasks_by_duration(min_duration, max_duration)`: Возвращает задачи, продолжительность которых находится в заданном диапазоне.
- `task_history()`: Возвращает историю изменений задач.
- `clear_completed_tasks()`: Удаляет все выполненные задачи.
- `list_recurring_tasks()`: Возвращает список периодических задач.
- `set_reminder(task_title, reminder_date)`: Устанавливает напоминание для задачи.
- `completion_percentage()`: Возвращает процент выполненных задач.
- `save_to_file(filename)`: Сохраняет список задач в файл.
- `load_from_file(filename)`: Загружает список задач из файла.

### Примеры использования
```python
from datetime import date, timedelta
from task_schedule import Task, Schedule

# Создание задач
task1 = Task(title="Buy groceries", description="Milk, Bread, Eggs", due_date=date.today() - timedelta(days=1))
task2 = Task(title="Submit assignment", description="Math assignment", due_date=date.today() + timedelta(days=2))

# Создание расписания и добавление задач
schedule = Schedule()
schedule.add_task(task1)
schedule.add_task(task2)

# Список просроченных задач
print(schedule.list_overdue_tasks())  # [Task(title='Buy groceries', description='Milk, Bread, Eggs', ...)]

# Список задач на сегодня
print(schedule.list_tasks_due_today())  # []

# Обновление задачи
schedule.update_task("Buy groceries", description="Milk, Bread, Eggs, Cheese", due_date=date(2024, 5, 26))

# Отметка задачи как выполненной
schedule.mark_as_completed("Buy groceries")
print(schedule.get_task("Buy groceries").status)  # "Completed"

# Список выполненных задач
print(schedule.list_completed_tasks())  # [Task(title='Buy groceries', description='Milk, Bread, Eggs, Cheese', ...)]

# Поиск задачи по ключевому слову
print(schedule.find_task_by_keyword("assignment"))  # [Task(title='Submit assignment', description='Math assignment', ...)]

# Проверка задач с дедлайном на завтра
print(schedule.check_deadlines())  # [Task(title='Submit assignment', description='Math assignment', ...)]

# Список всех задач
print(schedule.list_all_tasks())  # [Task(title='Buy groceries', ...), Task(title='Submit assignment', ...)]

# Добавление новой задачи с продолжительностью
task3 = Task(title="Water plants", description="Water the plants in the garden", due_date=date(2024, 5, 25), duration=2)
schedule.add_task(task3)
print(schedule.list_tasks_by_duration(1, 3))  # [Task(title='Water plants', description='Water the plants in the garden', ...)]

# История изменений задач
print(schedule.task_history())  # [('added', Task(...)), ...]

# Очистка выполненных задач
schedule.clear_completed_tasks()
print(schedule.list_all_tasks())  # [Task(title='Submit assignment', ...), Task(title='Water plants', ...)]

# Добавление новой периодической задачи
task4 = Task(title="Water plants", description="Water the plants in the garden", due_date=date(2024, 5, 25), recurrence="weekly")
schedule.add_task(task4)
print(schedule.list_recurring_tasks())  # [Task(title='Water plants', description='Water the plants in the garden', ...)]

# Установка напоминания для задачи
schedule.set_reminder("Submit assignment", date(2024, 5, 24))

# Процент выполнения задач
print(schedule.completion_percentage())  # 0.0

# Сохранение задач в файл
schedule.save_to_file("schedule.txt")

# Загрузка задач из файла
schedule.load_from_file("schedule.txt")
print(schedule.list_all_tasks())  # [Task(...), ...]
