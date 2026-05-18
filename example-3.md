### 5.1 Пример разделения видимости полей и метод классов

```python
class Auto:
    def __init__(self, auto_weight: int, auto_engine: Engine, auto_model: str, auto_length: int) -> None:
        self.__wight: int = auto_weight
        self.__luggage: int = 0
        self.__engine: Engine = auto_engine
        self.__model: str = auto_model
        self.__length: int = auto_length

    def get_into(self) -> None:
        self.__engine.start()

    def run(self) -> None:
        self.__engine.accelerate()

    def get_out(self) -> None:
        self.__engine.stop()

    def put_luggage(self, luggage: int) -> None:
        self.__luggage = luggage
        self.__wight += luggage

    def refuel(self, liters: int) -> None:
        self.__engine.stop()
        self.__engine.fill(liters)
        self.__engine.start()

class Engine:
    def __init__(self, engine_gas: int, engine_name: str, engine_power: int) -> None:
        self.__gas: int = engine_gas
        self.__name: str = engine_name
        self.__power: int = engine_power

    def __repr__(self) -> str:
        return f"Engine({self.__gas!r}, {self.__name!r}, {self.__power!r})"

    def start(self) -> None:
        self.__gas -= 1 # Предполагается что топливо уходит фоном

    def stop(self) -> None:
        self.__gas = self.__gas # Предполагается что уменьшение топлива останавливается

    def accelerate(self) -> None:
        self.__gas += 1

    def decelerate(self) -> None:
        self.__gas -= 3

    def fill(self, litres: int) -> None:
        self.__gas += litres
```

### 5.2 Пример пары небольших косвенно логически связанных иерархий классов
**Пример 1**: иерархия игрушек, от базовой к электронной и деревянной
```python
class Toy:
    def __init__(self, toy_name: str) -> None:
        self._name: str = toy_name

    def sound(self) -> None:
        pass

class Robot(Toy):
    def __init__(self, toy_name: str, battery: int) -> None:
        super().__init__(toy_name)
        self._battery = battery

    def sound(self) -> None:
        self._battery -= 1
        print("Бип-бип")

    def action(self) -> None:
        self._battery -= 3
        print("Танцуем")
        
    def fire(self) -> None:
        self._battery -= 3
        print("Запускаем ракеты из плечевой пушки")

class Whistle(Toy):
    def __init__(self, toy_name: str) -> None:
        super().__init__(toy_name)

    def sound(self) -> None:
        print("СВИСТ!")

    def disassemble(self) -> None:
        print("Разбираем на модули")
        
    def assemble(self) -> None:
        print("Собираем из модулей")
```

Пример 2: иерархия на примере сумки и её производных кейса, и сумки для инструментов.
```python
class Bag:
    def __init__(self, bag_size: int) -> None:
        self._bag_size = bag_size

class Case(Bag):
    def __init__(self, bag_size: int, resistance: str) -> None:
        super().__init__(bag_size)
        self._resistance = resistance
        self._password = ""

    def lock(self, case_password: str) -> None:
        self._password = case_password
        print("Закрыть кейс")

    def defend(self) -> None:
        self._resistance -= 1
        print("Защита от удара")

class ToolBag(Bag):
    def __init__(self, bag_size: int, pocket: int) -> None:
        super().__init__(bag_size)
        self._pocket = pocket
        
    def put_to_pocket(self) -> None:
        self._pocket += 1
        print("Положили инструмент в карман")
        
    def trim(self) -> None:
        self._bag_size -=1
        print("Использовали молниевые застёжки для укорочения размера сумки")
```
