
## Что такое указатель?

>**Указатель** — это тип переменной, который должен хранить адрес в памяти.

Я говорю здесь "должен", потому что если указатель правильно инициализирован, то в нем хранится либо `nullptr`, либо адрес другой переменной (он даже может хранить адрес другого указателя), но если он не был инициализирован должным образом, то в нем будут содержаться произвольные данные, что довольно опасно, так как это может привести к неопределенному поведению.

## Как можно инициализировать указатель?

В нашем распоряжении есть сразу три способа:

- Взять адрес другой переменной:

```cpp
#include <iostream>
int main(){  int v = 42;  int* p = &v;}
```

- Указать на переменную в куче

```cpp
#include <iostream>

int main(){ int* p = new int {42}; }
```

- Или просто взять значение другого указателя

```cpp
#include <iostream>
int main(){  int* p = new int {42};  int* p2 = p;}
```

## Значения указателей и значения, на которые они указывают

Если вы решите вывести на экран значение указателя, то вы увидите адрес в памяти. Но если вам необходимо получить значение, на которое указатель он указывает, то нужно **разыменовать** этот указатель с помощью оператора _._

```cpp
#include <iostream>

int main() {  
	int* p = new int {42};  
	int* p2 = p;  
	std::cout << p << " " << *p << '\n';
	std::cout << p2 << " " << *p2 << '\n';  
	std::cout << &p << " " << &p2 << '\n';
}
```

Вывод:

```
0x7d1848 42
0x7d1848 42
0x61ff0c 0x61ff08
```

В данном примере мы видим, что `p` и `p2` хранят один и тот же адрес в памяти, а это значит, что они указывают на одно и то же значение. Но если мы воспользуемся оператором `&`, то мы увидим, что адреса у этих указателей разные.

## Деаллокация памяти

Если выделение памяти (аллокация) происходит с помощью оператора `new`, другими словами, если вы выделяете память в куче, то кто-то должен впоследствии **высвободить** (деаллоцировать) выделенную память. Это можно сделать с помощью оператора `delete`. Если забыть это сделать, то, когда указатель выйдет за пределы области видимости, произойдет утечка памяти (memory leak). Поэтому обязательно высвобождайте всю выделенную память.

```cpp
#include <iostream>

int main() {
	int* p = new int {42};
	std::cout << p << " " << *p << '\n';
	delete p;
	}
```

Если вы попытаетесь получить доступ к указателю уже после удаления или же попытаетесь удалить его во второй раз, то это вызовет неопределенное поведение. Простейший способ перестраховаться от такой ситуации — сразу после удаления присвоить `p nullptr`. Если попытаться удалить указатель еще раз, то это не даст никакого эффекта, так как удаление `nullptr` является no-op.

```cpp
#include <iostream>

int main(){
	int* p = new int {42};
	std::cout << p << " " << *p << '\n';
	bool error = true;
	if (error) {
		delete p;
		p = nullptr;
		}
}
```

Еще один важный момент — всегда проверяйте пригодность (валидность) указателя перед обращением к нему. Что если указатель уже был удален и не установлен в `nullptr`? Неопределенное поведение, потенциальные краши. Или еще хуже...

## Итерация по массивам

Еще один важный момент, связанный с указателями, — это операции, которые можно выполнять над ними. Мы часто называем их арифметикой указателей, потому что указатели можно инкрементировать или декрементировать (выполнять сложение и вычитание). Но на самом деле можно складывать и вычитать любые целые числа... Благодаря возможности инкремента/декремента, указатели можно использовать для итерации по массивам и доступа к любому их элементу.

```cpp
#include <iostream>
int main(){
	int numbers[5] = {1, 2, 3, 4, 5};
	int* p = numbers;
	
	for(size_t i=0; i < 5; ++i) {
		std::cout << *p++ << '\n';
	}
	for(size_t i=0; i < 5; ++i) {
	    std::cout << *--p << '\n';
	}
	
	std::cout << '\n';
	std::cout << *(p+3) << '\n';
}
```

Это конечно хорошо, но стоит ли использовать указатели для итерации по массивам в 2023 году?

Ответ однозначен — нет. Это небезопасно, указатель может указывать куда угодно, и он не работает со всеми типами контейнеров.

В предыдущем примере вы могли заметить, что в первом цикле мы используем постфиксный инкремент, а во втором — префиксный декремент. После прохода по массиву указатель указывает на недопустимое местоположение, поэтому перед разыменованием его необходимо декрементировать, иначе мы рискуем наткнуться на неопределенное поведение.
