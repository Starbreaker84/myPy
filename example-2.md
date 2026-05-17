### Пример правильной организации классов
В данном примере классы спроектированы с точки зрения операций над этими классами.
Примеры намеренно упрощены, но, тем не менее, отражают основную суть - мы оперируем тем **что можно делать** с классами, а не их структурой.

**Пример 1**: класс двигателя, который может быть запущен, может работать с ускорением, может быть пополнен и может быть заглушен.

```python
class Auto:
    def __init__(self, auto_weight: int, auto_engine: Engine, auto_model: str, auto_length: int) -> None:
        self.wight: int = auto_weight
        self.luggage: int = 0
        self.engine: Engine = auto_engine
        self.model: str = auto_model
        self.length: int = auto_length

    def get_into(self) -> None:
        self.engine.start()
        
    def run(self) -> None:
        self.engine.accelerate()

    def get_out(self) -> None:
        self.engine.stop()

    def put_luggage(self, luggage: int) -> None:
        self.luggage = luggage
        self.wight += luggage

    def refuel(self, liters: int) -> None:
        self.engine.stop()
        self.engine.fill(liters)
        self.engine.start()
```

**Пример 2**: класс автомобиля, который можно активировать (условно, сесть в автомобиль), ехать, заправить, положить багаж и выйти из автомобиля.

```python
class Engine:
    def __init__(self, engine_gas: int, engine_name: str, engine_power: int) -> None:
        self.gas: int = engine_gas
        self.name: str = engine_name
        self.power: int = engine_power
        
    def start(self) -> None:
        self.gas -= 1 # Предполагается что топливо уходит фоном
        
    def stop(self) -> None:
        self.gas = self.gas # Предполагается что уменьшение топлива останавливается
        
    def accelerate(self) -> None:
        self.gas += 1 
        
    def decelerate(self) -> None:
        self.gas -= 3
        
    def fill(self, litres: int) -> None:
        self.gas += litres
```

Пример использования этих классов (игровая сюжетная поездка):

```python
    engine = Engine(50, "V8", 340)
    auto = Auto(960, engine, "Corolla", 345)
    
    auto.get_into()
    auto.put_luggage(30)
    auto.run()
    auto.refuel(5)
    auto.run()
    auto.get_out()
```

Стоит отметить, что хоть класс двигателя для нас скрыт внутри автомобиля, тем не менее, автомобиль общается с двигателем исключительно посредством сообщений, никак не взаимодействую с его структурой.
