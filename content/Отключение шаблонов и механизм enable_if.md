## Кратко:

>**`std::enable_if`** — это вспомогательный шаблон, предоставляемый в стандартной библиотеке C++ (в заголовке `<type_traits>`), позволяющий включать или исключать шаблоны из рассмотрения в зависимости от выполнения логического условия во время компиляции.

`std::enable_if` принимает два параметра: условие и тип. Если условие истинно (`true`), то тип определяется как второй параметр (обычно `void`). Если условие ложно (`false`), инстанцирование шаблона не происходит.

### Ключевые техники

- **Использование `std::enable_if` в качестве возвращаемого типа или параметра шаблона**: Основной способ применения `enable_if` — включение его в сигнатуру функции или шаблона класса.
- **Проверка типов с `std::is_*`**: Использование стандартных типовых проверок, таких как `std::is_arithmetic`, `std::is_integral` и других, для формирования условий в `enable_if`.

## Пример кода

### Пример 1: Отключение шаблонов с помощью `enable_if`

```cpp
#include <iostream>
#include <type_traits>

// Шаблон функции для числовых типов
template <typename T>
typename std::enable_if<std::is_arithmetic<T>::value, T>::type
add(T a, T b) {
    return a + b;
}

// Перегрузка функции для остальных типов
template <typename T>
typename std::enable_if<!std::is_arithmetic<T>::value, T>::type
add(T a, T b) {
    return T(); // Возвращает значение по умолчанию
}

int main() {
    std::cout << add(3, 4) << std::endl;         // 7 (числовые типы)
    std::cout << add(std::string("Hello, "), std::string("world!")) << std::endl; // пустая строка (остальные типы)
}
```

### Пример 2: Использование `enable_if` для ограничения специализаций класса

```cpp
#include <iostream>
#include <type_traits>

// Общий шаблон класса
template <typename T, typename Enable = void>
class MyClass;

// Специализация для числовых типов
template <typename T>
class MyClass<T, typename std::enable_if<std::is_arithmetic<T>::value>::type> {
public:
    void print() {
        std::cout << "Arithmetic type" << std::endl;
    }
};

// Специализация для остальных типов
template <typename T>
class MyClass<T, typename std::enable_if<!std::is_arithmetic<T>::value>::type> {
public:
    void print() {
        std::cout << "Non-arithmetic type" << std::endl;
    }
};

int main() {
    MyClass<int> numType;
    numType.print(); // Arithmetic type

    MyClass<std::string> nonNumType;
    nonNumType.print(); // Non-arithmetic type
}
```
