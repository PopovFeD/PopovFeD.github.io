Шаблон класса `Stack` позволяет создавать стеки с элементами любого типа. Основные свойства стека:

- Последний пришел — первый ушел (LIFO).
- Операции `push` и `pop` выполняются за постоянное время.
- Внутреннее хранение может быть реализовано на основе массива или связного списка.

## Пример кода

```cpp
#include <iostream>
#include <vector>

template<typename T>
class Stack {
private:
    std::vector<T> elements; // Внутреннее хранение на основе std::vector

public:
    // Добавление элемента в стек
    void push(const T& value) {
        elements.push_back(value);
    }

    // Удаление верхнего элемента из стека
    void pop() {
        if (!elements.empty()) {
            elements.pop_back();
        } else {
            throw std::out_of_range("Stack<>::pop(): empty stack");
        }
    }

    // Получение верхнего элемента без удаления
    T top() const {
        if (!elements.empty()) {
            return elements.back();
        } else {
            throw std::out_of_range("Stack<>::top(): empty stack");
        }
    }

    // Проверка, пуст ли стек
    bool isEmpty() const {
        return elements.empty();
    }

    // Получение размера стека
    size_t size() const {
        return elements.size();
    }
};

int main() {
    Stack<int> intStack;  // Стек для целых чисел

    intStack.push(1);
    intStack.push(2);
    intStack.push(3);

    std::cout << "Top element: " << intStack.top() << std::endl; // Вывод: 3

    intStack.pop();
    std::cout << "Top element after pop: " << intStack.top() << std::endl; // Вывод: 2

    std::cout << "Stack size: " << intStack.size() << std::endl; // Вывод: 2

    return 0;
}
```
