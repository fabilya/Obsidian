**Методы класса** принимают класс в качестве параметра; этот параметр принято называть `cls`. Этот параметр указывает на сам класс, а не на объект этого класса. При описании метода класса применяется декоратор `@classmethod`.

Методы класса привязаны к самому классу, а не его экземпляру. Они могут менять состояние класса, и это отразится на всех объектах этого класса; методы класса не могут менять конкретный экземпляр.

Как правило, метод класса используют в том случае, когда нужен генерирующий метод, возвращающий объект класса.
___
**Статические методы** описываются при помощи декоратора `@staticmethod`. Им не нужен определённый аргумент (ни `self`, ни `cls`). Их можно воспринимать как методы, которые «не знают, к какому классу относятся». Таким образом, статические методы прикреплены к классу лишь для удобства и не могут менять состояние ни класса, ни его экземпляра.

Статические методы в основном используются как вспомогательные функции и работают с данными, которые им переданы.