*Links*: [[00 - Index|Index]]
*Date*: 28.09.2024
*Resources*: [name]()

---

## Shorthand Operators
* ### Post-Increment (intVar++)
	* Değişkenin bir yedeği alınır (backup).
	* Sonra değişken 1 artırılır.
	* Alınmış yedek geri döndürülür.
	* Örnek C kodu:
		```c
		int postInc(int *num) {
			int backup = *num;
			*num = *num + 1;
			return backup;
		}
		```

* ### Pre-Increment (++intVar)
	* Değişkenin bir yedeği alınmaz (backup).
	* Değişken bir artırılır ve geri döndürülür.
	* Örnek C kodu:
		```c
		int preInc(int *num) {
			*num = *num + 1;
			return *num;
		}
		``` 
## Console Input/Output 
* `<iostream>` kütüphanesi kullanılır.
* Bu satırlar i/o için mutlaka olmalıdır:
	```cpp
		#include <iostream>  
		using namespace std;
	```
* cin : Input
* cout: Output
* cerr: Error output
* ### [[01.01 - Akış Operatörü|<< Operatörü]]
	* Veriyi bir çıkış akışına (output stream) eklemek için kullanılır
	* Ör: 
	 ```cpp
		std::cout << "Value of x: " << x << ", Value of y: " << y << std::endl;
	```
	
	
## Strings
* Cpp karakter verilerini saklamak için kendi `string` veri tipine sahiptir.
* Primitve bir veri tipi değildir.
* `<string>` kütüphanesi kullanılır.
* `+` Operatörü iki string'i birleştirir.
* Örnek:
	```cpp
		string str1;
		cin >> str1; // Input
		cout << str1; // Output
	```
## Formatting numbers
* C++ dilinde sayıları formatlamak için cout metodlarını kullanırız. Ör:
	```cpp
		cout.setf(ios::fixed);  
		cout.setf(ios::showpoint);  
		cout.precision(2);
	```
* Ama C dilinde bulunan `printf` fonksiyonunu da kullanabiliriz.