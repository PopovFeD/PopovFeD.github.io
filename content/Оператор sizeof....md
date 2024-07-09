## Кратко:

Оператор `sizeof...` вычисляет количество аргументов в пакете параметров шаблона и возвращает это значение как константное выражение `std::size_t`.

### Синтаксис

```cpp
template<typename... Args>
void function(Args... args) {
    constexpr std::size_t numArgs = sizeof...(Args);
    // ...
}
```

---

## Пример кода: Условное выполнение в зависимости от количества аргументов

```cpp
#include <iostream>

template<typename... Args>
void processArguments(Args... args) {
    if constexpr (sizeof...(Args) == 0) {
        std::cout << "No arguments provided." << std::endl;
    } else {
        std::cout << "Processing " << sizeof...(Args) << " arguments." << std::endl;
        // Дополнительная обработка аргументов
    }
}

int main() {
    processArguments();                 // Output: No arguments provided.
    processArguments(1, 2, 3);          // Output: Processing 3 arguments.
    processArguments("Hello", 'A');     // Output: Processing 2 arguments.

    return 0;
}
```
