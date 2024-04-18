Намного удобнее работать с готовыми библиотеками для тестирования. Вот самые популярные в Python (по алфавиту, чтобы никого не обидеть):

-   **nose2**
-   **pytest**
-   [**unittest**](https://docs.python.org/3/library/unittest.html) — стандартная библиотека Python, с ней и будем работать.

## Топ-дюжина методов класса TestCase

Кроме метода `assertEqual` в Unittest есть множество других методов на все случаи жизни.

Вот несколько самых популярных:
[assertEqual(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertEqual) a == b
[assertNotEqual(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotEqual) a != b
[assertTrue(x)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertTrue) bool(x) is True
[assertFalse(x)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertFalse) bool(x) is False
[assertIs(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIs) a is b
[assertIsNot(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsNot) a is not b
[assertIsNone(x)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsNone) x is None
[assertIsNotNone(x)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsNotNone) x is not None
[assertIn(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIn) a in b
[assertNotIn(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotIn) a not in b
[assertIsInstance(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsInstance) isinstance(a, b)
[assertNotIsInstance(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotIsInstance) not isinstance(a, b)
Все эти методы могут в качестве необязательного последнего аргумента содержать текст сообщения об ошибке.

Другие методы (их список постоянно пополняется) можно найти [в официальной документации библиотеки _Unittest_](https://docs.python.org/3/library/unittest.html#unittest.TestCase.debug).

[django](https://docs.djangoproject.com/en/4.1/topics/testing/tools/)




## Управление тестами

**Unittest** позволяет пропускать (не выполнять) классы тестов и отдельные тесты. Для этого в библиотеке есть специальные декораторы:

-   @**unittest.skip**(**reason**) — пропустить тест. В параметре `reason` описывается причина пропуска.
-  @**unittest.skipIf(condition, reason)** — пропустить тест, если условие `condition` истинно.
-   @**unittest.skipUnless(condition, reason)** — пропустить тест, если условие `condition` ложно.

Можно отмаркировать тест меткой «тест не работает, но это так и задумано».

-   @**unittest.expectedFailure** — ставит на тесте отметку «ожидаемая ошибка».




### Объект **response: о**твет на запрос

При запросе клиента возвращается специальный объект **response**. В нём содержится ответ сервера и дополнительная информация:

-   `status_code` — содержит код ответа запрошенного адреса;
-   `client` — объект клиента, который использовался для обращения;
-   `content` — данные ответа в виде строки байтов;
-   `context` — словарь переменных, переданный для отрисовки шаблона при вызове функции `render()`;
-   `request` — объект `request`, первый параметр view-функции, обработавшей запрос;
-   `templates` — перечень шаблонов, вызванных для отрисовки запрошенной страницы;
-   `resolver_match` — специальный объект, соответствующий `path()` из списка `urlpatterns`.