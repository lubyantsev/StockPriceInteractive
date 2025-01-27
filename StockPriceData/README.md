# Анализ и визуализация данных об акциях

## Ссылка на проект

[Ссылка на проект](https://github.com/lubyantsev/StockPriceInteractive)

## Общий обзор

Этот проект предназначен для загрузки и визуализации исторических данных об акциях, используя библиотеку yfinance для
получения данных и matplotlib для создания графиков. Пользователи могут выбирать различные тикеры и временные периоды
для анализа, а также просматривать движение цен и скользящие средние на графике. Проект помогает не только в
визуализации данных, но и в их анализе, предоставляя возможность отслеживания колебаний цен.

## Структура и модули проекта

1. **data_download.py**:
    - Ответственный за загрузку данных об акциях.
    - Содержит функции для извлечения данных из интернета и вычисления скользящего среднего, индекса относительной
      силы (RSI) и MACD с сигнальной линией.

2. **main.py**:
    - Точка входа в программу.
    - Запрашивает у пользователя тикер акции и временной период, загружает и обрабатывает данные, а затем визуализирует
      результаты.

3. **data_plotting.py**:
    - Отвечает за визуализацию данных.
    - Содержит функции для создания и сохранения графиков цен закрытия и скользящих средних, а также графиков RSI,
      MACD и графика полос Боллинджера.

4. **data_analysis.py**:
    - Содержит функции для анализа данных.
    - Позволяет рассчитывать среднюю цену закрытия и уведомляет о сильных колебаниях цен.
    - Включает функцию export_data_to_csv для экспорта данных о ценах акций в CSV файл.
    - Добавлены функции для расчета стандартного отклонения (calculate_standard_deviation)
      и полос Боллинджера (calculate_bollinger_bands), которые помогают анализировать волатильность и тренды цен акций.

5. **interactive_graph.py**:
    - Модуль отвечает за создание интерактивных графиков с использованием библиотеки Plotly.
    - Содержит функцию plot_interactive_graph, которая принимает данные по акциям (stock_data), тикер (ticker),
      временной период (period) или диапазон дат (start_date и end_date), и строит интерактивный график цены закрытия
      акций с добавлением средней линии.
    - Функция проверяет наличие столбца 'Close' в переданных данных, рассчитывает среднее значение цены закрытия и
      отображает его на графике в виде пунктирной линии.
    - Интерактивность позволяет пользователю исследовать динамику изменения цен акций более детально.

6. **chart_styles.py**
    - Этот модуль предоставляет функционал для работы со стилями графиков Matplotlib.
    - Он выводит список всех доступных стилей графиков, позволяя разработчику выбрать подходящий стиль для визуализации
      данных.
    - Это помогает улучшить внешний вид графиков и сделать их более читабельными и эстетичными.

## Описание функций

### 1. data_download.py:

- **fetch_stock_data(ticker, period='1mo')**:
  Получает исторические данные об акциях для указанного тикера и временного периода.

- **add_moving_average(data, window_size=5)**:
  Добавляет в DataFrame колонку со скользящим средним, рассчитанным на основе цен закрытия.

- **calculate_rsi(data, window=14)**:
  Рассчитывает индекс относительной силы (RSI) для анализа динамики цен.

- **calculate_macd(data, short_window=12, long_window=26, signal_window=9)**:
  Рассчитывает MACD и сигнальную линию для анализа трендов.

### 2. main.py:

- **main()**:
  Основная функция, управляющая процессом загрузки, обработки данных и их визуализации, запрашивая у пользователя ввод
  данных и вызывая соответствующие функции.

### 3. data_plotting.py:

- **create_and_save_plot(data, ticker, period, filename=None)**:
  Создаёт график, отображающий цены закрытия и скользящие средние, индекс относительной силы (RSI), MACD и сигнальную
  линию, с возможностью сохранения графика в файл.

### 4. data_analysis.py:

- **calculate_and_display_average_price(data)**:
  Рассчитывает и отображает среднюю цену закрытия за указанный период.

- **notify_if_strong_fluctuations(data, threshold)**:
  Уведомляет, если цены акций колебались более чем на заданный процент.

- **export_data_to_csv(data, filename)**:
  Экспортирует данные о ценах акций в CSV файл в папку csv_files.

- **calculate_standard_deviation(stock_data, window=20)**:
  Вычисляет стандартное отклонение цен закрытия.

- **calculate_bollinger_bands(stock_data, window=20, num_std_dev=2)**:
  Вычисляет полосы Боллинджера для цен закрытия.

### 5. interactive_graph.py:

- **plot_interactive_graph(stock_data, ticker, period=None, start_date=None, end_date=None)**: Создаёт интерактивный
  график цены закрытия акций с помощью библиотеки Plotly. Принимает DataFrame с данными акций (stock_data), тикер (
  ticker), временной период (period) или диапазон дат (start_date и end_date). Проверяет наличие столбца 'Close' в
  переданном DataFrame. Рассчитывает среднее значение цены закрытия и добавляет его на график в виде пунктирной линии.
  Формирует заголовок графика на основании переданного периода или диапазона дат. Отображает интерактивный график,
  позволяющий пользователю исследовать динамику изменения цен акций.

### 6. chart_styles.py:

- **list_available_styles()**: Выводит список всех доступных стилей графиков, предоставляемых библиотекой Matplotlib.
  Помогает выбрать подходящий стиль для улучшения внешнего вида и читаемости графиков.

## Пошаговое использование

Этот проект предоставляет пользователю возможность анализировать и визуализировать исторические данные акций. Следуйте
этим шагам, чтобы начать работу с проектом:

### Шаг 1: Установка необходимых библиотек

Убедитесь, что у вас установлены необходимые библиотеки. Вы можете установить их с помощью pip:

```bash
pip install yfinance matplotlib pandas plotly
```

### Шаг 2: Запуск программы

1. Откройте файл `main.py` в вашем IDE (например, PyCharm).
2. Запустите файл с помощью команды:

```bash
python main.py
```

### Шаг 3: Ввод данных

После запуска программы вы увидите приветственное сообщение с инструкциями:

- Введите тикер акции, который вы хотите проанализировать (например, AAPL для акций Apple).
- Вам будет предложено использовать конкретные даты начала и окончания для получения данных. Если вы хотите это сделать,
  введите "да" и затем укажите даты в формате YYYY-MM-DD. Если нет, просто введите "нет" и укажите период для получения
  данных (например, 1mo для данных за один месяц).
- Вам будет предложено выбрать стиль графика. Вы можете выбрать один из доступных стилей для настройки визуализации.
- Введите порог для уведомления о колебаниях в процентах (например, 5 для 5%).
- Программа автоматически загрузит данные о выбранной акции за указанный период или указанные даты.
- После анализа данных вы сможете ввести имя файла для экспорта полученных данных в CSV формате (например,
  stock_data.csv). Если экспорт не нужен, просто нажмите Enter.

### Шаг 4: Просмотр результатов

После ввода данных программа выполнит следующие действия:

1. Загрузит данные о выбранной акции за указанный период.
2. Рассчитает скользящее среднее и добавит его в набор данных.
3. Создаст интерактивный график, на котором будут отображены цены закрытия и скользящие средние, и сразу же отобразит
   его для анализа.
4. Создаст график RSI, MACD и сохранит их, чтобы помочь в анализе.
5. Создаст и сохранит график с полосами Боллинджера, который позволит визуально оценить волатильность цен акций.
6. Рассчитает и отобразит среднюю цену закрытия за указанный период.
7. Уведомит вас о сильных колебаниях цен, если они превышают заданный вами порог.
8. Экспортирует данные о ценах акций в CSV файл.

### Шаг 5: Просмотр графиков

После завершения работы программы вы можете найти графики в папке `charts` в вашем проекте. Имена файлов будут
сгенерированы
автоматически, основываясь на тикере и периоде.

### Шаг 6: Анализ данных

Используйте полученные результаты для анализа поведения цен акций. Вы можете повторять процесс с разными тикерами и
периодами, чтобы исследовать различные тренды и колебания на рынке.

### Примечания

- Убедитесь, что вы используете актуальные тикеры акций, так как устаревшие или неверные тикеры могут привести к ошибкам
  при загрузке данных.
- Проверяйте консоль на наличие сообщений об ошибках, если данные не загружаются или возникают другие проблемы.
- Для более глубокого анализа вы можете модифицировать функции в `data_analysis.py` или добавлять новые функции в
  зависимости от ваших потребностей.