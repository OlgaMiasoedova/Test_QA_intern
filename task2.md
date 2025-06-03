# Задача Playwright:

## Условие:

Написать тест, который открывает веб-страницу https://playwright.dev/ и проверяет что заголовок страницы соответствует ожидаемому значению. Тест необходимо запустить минимум на 2 разных браузерах.

## Ожидаемый результат:

Тест, успешно проходящий проверку заголовка.

## Решение:

```ruby
from playwright.sync_api import Playwright, sync_playwright, expect


def run(playwright: Playwright, browser_type):
    print(f"Тест в браузере: {browser_type}")
    browser = getattr(playwright, browser_type).launch(headless=True)
    context = browser.new_context()
    page = context.new_page()
    page.goto('https://playwright.dev/')
    expected_title = "Playwright enables reliable end-to-end testing for modern web apps."
    actual_title = page.title()
    assert actual_title == expected_title, f"Ожидали '{expected_title}', получили '{actual_title}'"
    context.close()
    browser.close()
    print(f"Успешно в {browser_type}\n")


with sync_playwright() as playwright:
    for browser_name in ["chromium", "firefox"]:
        run(playwright, browser_name)
```
