# Документация API

Класс `api` предоставляет набор статических методов для управления объектами, камерой, сценой, глобальными переменными и вводом.

Все методы вызываются через класс, например:

```python
api.move(ctx, 10, 0)
```

## Общие соглашения

- `ctx` — ключ или индекс объекта в коллекции `objects`.
- `ctx2` — второй объект для проверки столкновения.
- `uuid` — строковый идентификатор объекта.
- Методы, которые ничего не возвращают явно, возвращают `None`.

## Зависимости

Для работы API предполагаются доступными:

- `objects` — коллекция объектов;
- `global_variables` — словарь глобальных переменных;
- `camera_dx`, `camera_dy` — смещение камеры;
- `target_scene_id` — идентификатор целевой сцены;
- `pygame`;
- `keyboard`.

---

## Быстрый справочник

| Метод | Назначение |
|---|---|
| `move` | Сместить объект на заданное значение |
| `moveTo` | Переместить объект в координаты |
| `transform` | Изменить размер объекта |
| `pressedKey` | Проверить нажатие клавиши |
| `getAttribute` | Получить атрибут объекта |
| `setCustomAttribute` | Установить пользовательский атрибут |
| `getCustomAttribute` | Получить пользовательский атрибут |
| `hide` | Скрыть или показать объект |
| `setGlobal` | Установить глобальную переменную |
| `getGlobal` | Получить глобальную переменную |
| `setCamera` | Установить смещение камеры |
| `setTexture` | Установить текстуру объекта |
| `getTextureName` | Получить имя текстуры объекта |
| `getCamera` | Получить смещение камеры |
| `getScene` | Получить текущую целевую сцену |
| `setScene` | Установить целевую сцену |
| `isCollide` | Проверить столкновение двух объектов |
| `isMouseCollide` | Проверить столкновение объекта с мышью |
| `getMousePos` | Получить позицию мыши |
| `getUuid` | Получить UUID объекта |
| `getCtxOfUuid` | Найти объект по UUID |

---

## Методы

### `move(ctx, x, y)`

```python
api.move(ctx: int, x: int, y: int) -> None
```

Смещает объект `ctx` по осям X и Y.

**Параметры:**

- `ctx` — объект, который нужно переместить.
- `x` — смещение по X.
- `y` — смещение по Y.

**Пример:**

```python
api.move(ctx, 5, -3)
```

---

### `moveTo(ctx, x, y)`

```python
api.moveTo(ctx: int, x: int, y: int) -> None
```

Перемещает объект `ctx` в указанные координаты.

**Параметры:**

- `ctx` — объект.
- `x` — новая координата X.
- `y` — новая координата Y.

**Пример:**

```python
api.moveTo(ctx, 100, 200)
```

---

### `transform(ctx, width, height)`

```python
api.transform(ctx: int, width: int, height: int) -> None
```

Изменяет ширину и высоту объекта.

**Параметры:**

- `ctx` — объект.
- `width` — новая ширина.
- `height` — новая высота.

**Пример:**

```python
api.transform(ctx, 64, 64)
```

---

### `pressedKey(key)`

```python
api.pressedKey(key: str) -> bool
```

Проверяет, нажата ли указанная клавиша.

**Параметры:**

- `key` — название клавиши, например `"space"`, `"a"`, `"left"`.

**Возвращает:**

- `True` — клавиша нажата.
- `False` — клавиша не нажата.

**Пример:**

```python
if api.pressedKey("space"):
    print("Прыжок")
```

---

### `getAttribute(ctx, attr)`

```python
api.getAttribute(ctx: int, attr: str) -> any
```

Возвращает значение атрибута объекта.

**Параметры:**

- `ctx` — объект.
- `attr` — имя атрибута.

**Возвращает:**

- Значение атрибута или `None`, если атрибут отсутствует.

**Пример:**

```python
x = api.getAttribute(ctx, "x")
```

---

### `setCustomAttribute(ctx, attr, value)`

```python
api.setCustomAttribute(ctx: int, attr: str, value: any) -> None
```

Устанавливает пользовательский атрибут объекта.

**Параметры:**

- `ctx` — объект.
- `attr` — имя пользовательского атрибута.
- `value` — значение.

**Пример:**

```python
api.setCustomAttribute(ctx, "health", 100)
```

---

### `getCustomAttribute(ctx, attr)`

```python
api.getCustomAttribute(ctx: int, attr: str) -> any
```

Возвращает пользовательский атрибут объекта.

**Параметры:**

- `ctx` — объект.
- `attr` — имя пользовательского атрибута.

**Возвращает:**

- Значение пользовательского атрибута или `None`, если атрибут отсутствует.

**Пример:**

```python
health = api.getCustomAttribute(ctx, "health")
```

---

### `hide(ctx, value)`

```python
api.hide(ctx: int, value: any) -> None
```

Управляет видимостью объекта через атрибут `hide`.

**Параметры:**

- `ctx` — объект.
- `value` — значение скрытия. Обычно `True` — скрыть, `False` — показать.

**Пример:**

```python
api.hide(ctx, True)
```

---

### `setGlobal(name, value)`

```python
api.setGlobal(name: str, value: any) -> None
```

Устанавливает глобальную переменную.

**Параметры:**

- `name` — имя глобальной переменной.
- `value` — значение.

**Пример:**

```python
api.setGlobal("score", 10)
```

---

### `getGlobal(name)`

```python
api.getGlobal(name: str) -> any
```

Возвращает значение глобальной переменной.

**Параметры:**

- `name` — имя глобальной переменной.

**Возвращает:**

- Значение переменной или `None`, если переменной нет.

**Пример:**

```python
score = api.getGlobal("score")
```

---

### `setCamera(dx, dy)`

```python
api.setCamera(dx: int, dy: int) -> None
```

Устанавливает смещение камеры.

**Параметры:**

- `dx` — смещение камеры по X.
- `dy` — смещение камеры по Y.

**Пример:**

```python
api.setCamera(10, 0)
```

---

### `setTexture(ctx, texture)`

```python
api.setTexture(ctx: int, texture: str) -> None
```

Устанавливает текстуру объекта.

**Параметры:**

- `ctx` — объект.
- `texture` — имя или путь текстуры.

**Пример:**

```python
api.setTexture(ctx, "player.png")
```

---

### `getTextureName(ctx)`

```python
api.getTextureName(ctx: int) -> str
```

Возвращает имя текущей текстуры объекта.

**Параметры:**

- `ctx` — объект.

**Возвращает:**

- Имя текстуры.

**Пример:**

```python
texture = api.getTextureName(ctx)
```

---

### `getCamera()`

```python
api.getCamera() -> tuple[int, int]
```

Возвращает текущее смещение камеры.

**Возвращает:**

- Кортеж `(camera_dx, camera_dy)`.

**Пример:**

```python
dx, dy = api.getCamera()
```

---

### `getScene()`

```python
api.getScene() -> int
```

Возвращает идентификатор целевой сцены.

**Возвращает:**

- `target_scene_id`.

**Пример:**

```python
scene = api.getScene()
```

---

### `setScene(scene)`

```python
api.setScene(scene: int) -> None
```

Устанавливает идентификатор целевой сцены.

**Параметры:**

- `scene` — ID сцены.

**Пример:**

```python
api.setScene(2)
```

---

### `isCollide(ctx, ctx2)`

```python
api.isCollide(ctx: int, ctx2: int) -> bool
```

Проверяет столкновение двух объектов по их прямоугольникам.

**Параметры:**

- `ctx` — первый объект.
- `ctx2` — второй объект.

**Возвращает:**

- `True` — объекты пересекаются.
- `False` — объекты не пересекаются.

**Пример:**

```python
if api.isCollide(player, enemy):
    print("Столкновение")
```

---

### `isMouseCollide(ctx, btn)`

```python
api.isMouseCollide(ctx: int, btn: int) -> bool
```

Проверяет столкновение прямоугольника объекта с позицией мыши.

В текущей реализации `btn` используется как индекс координаты в `pygame.mouse.get_pos()`:

- `0` — X;
- `1` — Y.

> Внимание: в таком виде в `collidepoint` передаётся только одна координата, а не пара `(x, y)`. Это выглядит как ошибка. Для проверки наведения мыши на объект обычно нужно использовать полную позицию `pygame.mouse.get_pos()`.

**Параметры:**

- `ctx` — объект.
- `btn` — индекс координаты мыши: `0` или `1`.

**Возвращает:**

- `True` — есть столкновение.
- `False` — нет столкновения.

**Пример:**

```python
if api.isMouseCollide(ctx, 0):
    print("Курсор рядом")
```

---

### `getMousePos()`

```python
api.getMousePos() -> tuple[int, int]
```

Возвращает текущую позицию мыши.

**Возвращает:**

- Кортеж `(x, y)`.

**Пример:**

```python
mx, my = api.getMousePos()
```

---

### `getUuid(ctx)`

```python
api.getUuid(ctx: int) -> str
```

Возвращает UUID объекта.

**Параметры:**

- `ctx` — объект.

**Возвращает:**

- UUID объекта.

**Пример:**

```python
uuid = api.getUuid(ctx)
```

---

### `getCtxOfUuid(uuid)`

```python
api.getCtxOfUuid(uuid: str) -> int | None
```

Ищет объект по UUID и возвращает его индекс в коллекции `objects`.

**Параметры:**

- `uuid` — UUID объекта.

**Возвращает:**

- Индекс объекта, если он найден.
- `None`, если объект не найден.

**Пример:**

```python
ctx = api.getCtxOfUuid("some-uuid")
if ctx is not None:
    api.move(ctx, 1, 0)
```

---

## Примечания

1. Метод `isMouseCollide` в текущем виде, вероятно, работает некорректно, так как передаёт в `collidepoint` только одну координату.
2. Метод `getCtxOfUuid` предполагает, что `objects` — индексируемая коллекция, например список, а её элементы — словари с ключом `"uuid"`.
3. Методы `setCustomAttribute` и `getCustomAttribute` работают с вложенным словарём `objects[ctx]["custom"]`.
