### 5.1 Пакеты

Поулчилась вот такая структура пакетов:

![packages](https://github.com/Starbreaker84/myPy/blob/main/Screenshot%202026-05-22%20162857.png)

Класс Item:
```python
class Item:
    def __init__(self, item_id: str, item_name: str, item_price: float) -> None:
        self.id: str = item_id
        self.name: str = item_name
        self.price: float = item_price

    def __repr__(self) -> str:
        return f"{{ Номер товара: {self.id}, название: {self.name}, стоимость: {self.price} }}"
```

Класс Order, который импортирует Item
```python
from datetime import datetime

from example.item.item import Item


class Order:
    def __init__(self, order_id: str, order_items: list[Item]):
        self.id: str = order_id
        self.created_at: datetime = datetime.now()
        self.items: list[Item] = order_items
        self.quantity = order_items.__len__()

    def add_item(self, item: Item):
        self.items.append(item)
        self.quantity += 1

    def remove_item(self, item: Item):
        self.items.remove(item)
        if self.quantity > 0:
            self.quantity -= 1
```

И основной класс программы, который импортирует классы из обоих пакетов:
```python
from example.item.item import Item
from example.order.order import Order


def main():
    item: Item = Item("3445", "Шкаф", 345.87)
    items: list[Item] = [item]
    order: Order = Order("576dgdgdh", items)

    print(f"Заказ №{order.id} был создан {order.created_at:%Y-%m-%d} в {order.created_at:%H:%M:%S}")
    print(f"Содержание заказа: {order.items}")

if __name__ == "__main__":
    main()
```

### 5.2 Форматированный вывод
Вот такой красивый вывод можно делать:
![format](https://github.com/Starbreaker84/myPy/blob/main/Screenshot%202026-05-22%20162658.png)
