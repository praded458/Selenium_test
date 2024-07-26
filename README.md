<h2> Cоздания авто теста Python Selenium</h2>

# Работа в VS установка Python
https://www.python.org/downloads/
в VS установть расшерение Python

# Установка необходимых модулей

'pip install pytest'
'pip install selenium'
'pip install allure-pytest'

# Создание и активация виртуального окружения
Выполнять в командной строке в корне проекта
Создаем виртуальное окружение
'python -m venv env   # возможно не python, а python3'

# Активируем окружение
cd до папки с виртуальным окружением

'.\env\Scripts\Activate.ps1' # команда для Windows
'source env/bin/activate'    # команда для Linux

# Деактивация окружения
'deactivate'

# Запуск созданного теста можно осуществить двумя способами: 
Из командной строки: 
'pytest tests/test_smoke.py::test_product_view_sku'

# а вот так с сохранением отчетов в формате allure
'pytest tests/test_smoke.py::test_product_view_sku --alluredir=my_allure_results'

## Как ожидать появление объекта

Вприсываем скрипт

'def test_USER_TEST(browser):
    """
    Test case №
    """
    browser.get(URL) #переменная входящего урла

    browser.execute_script("window.scrollTo(0, document.body.scrollHeight);") #Скролим страницу по всей высоте

    WebDriverWait(browser, timeout=10, poll_frequency=2).until(EC.text_to_be_present_in_element(
        (By.CLASS_NAME, "razzi-posts__found"), "ИЩЕМ ЮЗЕР ТЕКСТ"))
    #ждем 10 сек с проверкой каждые 2 сек, ищем текст по условию
    elements = browser.find_elements(by=By.CSS_SELECTOR, value="[id='rz-shop-content'] ul li")
    #поиск по селекторам
    assert len(elements) == 17, "Unexpected count of products" #сравниваем колличество элемнтов на странице с заданными.'

## Запустить сервер отчетов командой: 
'cd <путь до каталог allure\bin> (первая команда)
.\allure.bat (вторая)
.\allure serve <путь до каталога с результатами> (третья)

В моем случае это получилось так:
cd i:\github\allure-2.9.0\bin\
.\allure.bat
.\allure serve I:\github\selenium.qa.studio\my_allure_results

Для MacOS (если установил allure через brew)
allure serve /Users/gdolnikov/projects/selenium.qa.studio/my_allure_results

my_allure_results — это ты сам создаешь или выбираешь в какую папку смотреть allure-у для создания красивого дашборда

Итогом выполнения последней команды будет запуск и открытие в браузере страницы с отчетами'

Автор Сергей Авдеев
