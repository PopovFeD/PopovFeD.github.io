## Поиск, зависящий от аргумента (Argument-Dependent Lookup, ADL)

>**ADL** — это механизм, позволяющий компилятору находить функции, исходя из типов аргументов, переданных в вызове функции. Это особенно полезно при использовании пространств имен, так как ADL помогает автоматически находить и вызывать правильные функции, определенные в этих пространствах имен.

## Пример использования ADL

Рассмотрим пример, демонстрирующий ADL в действии:

```cpp
#include <iostream>

namespace MyNamespace {
    class MyClass {};
    
    void myFunction(MyClass) {
        std::cout << "Function found via ADL in MyNamespace!" << std::endl;
    }
}

int main() {
    MyNamespace::MyClass obj;
    myFunction(obj); // ADL находит MyNamespace::myFunction
    return 0;
}
```

## Объяснение

- **Определение функции в пространстве имен:** Функция `myFunction` определена в пространстве имен `MyNamespace`.
- **Создание объекта:** В `main` создается объект `obj` типа `MyNamespace::MyClass`.
- **Вызов функции:** Вызов `myFunction(obj)` не указывает явно пространство имен. Вместо этого, благодаря ADL, компилятор находит функцию `myFunction` в пространстве имен `MyNamespace`, так как тип аргумента `MyClass` находится в этом пространстве имен.

## ADL в перегрузке функций

ADL также работает при перегрузке функций, что делает его полезным для функций, которые должны работать с типами, определенными в различных пространствах имен.

```cpp
#include <iostream>

namespace MyNamespace {
    class MyClass {};
    
    void myFunction(MyClass) {
        std::cout << "Function with MyClass found via ADL!" << std::endl;
    }

    void myFunction(int) {
        std::cout << "Function with int found via ADL!" << std::endl;
    }
}

int main() {
    MyNamespace::MyClass obj;
    myFunction(obj); // ADL находит MyNamespace::myFunction(MyClass)
    myFunction(42);  // ADL не применяется, будет ошибка компиляции (если не объявлена глобальная функция)
    return 0;
}
```

## Важные моменты

- **Область видимости:** ADL учитывает пространства имен, связанные с типами аргументов, передаваемых в функцию.
- **Неявный поиск:** ADL работает автоматически, облегчая вызов функций, определенных в пространствах имен, без явного указания этих пространств.
