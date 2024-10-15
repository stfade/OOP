*Links*: [[00 - Index|Index]]
*Date*: 01.10.2024
*Resources*: [name]()

---
# Parameters
## Call-by-value
* Değerin (argument) bir kopyası gönderilir.
* Fonksiyon içinde yerel değişken olarak kabul edilir.
* Eğer değer değiştirilse sadece local olarak bir değişim olur. Bir üst scope'u etkilemez.
* Ör:
```cpp
	#include <iostream>
	
	// Değer ile çağırma örneği
	void increment(int num) {
	    num = num + 1; // num değişkeninin kopyası üzerinde işlem yapılır
	    std::cout << "Inside function: " << num << std::endl;
	}
	 
	int main() {
	    int a = 5;
	    increment(a); // a değişkeninin değeri fonksiyona kopyalanır
	    std::cout << "Outside function: " << a << std::endl; // a değişkeninin değeri değişmez 
	    return 0;
	
	}
```
## Call-by-reference
* Değerin bulunduğu adres gönderilir.
* Fonksiyonun çağırıldığı yerdeki gerçek değere erişim için kullanılır.
* Fonksiyonun çağırıldığı yerdeki değer, fonksiyon içinde değiştirilebilir. Çünkü bu işlemi doğrudan bellekteki değeri değiştirerek yapar.
* Argüman olarak bellek değeri gönderilir.
* `&` işareti ile belirtilir.
* Referans argümanları doğası gereği tehlikelidir. Çünkü gerçek değer değiştirilir ve bu bazen gözden kaçan bir durum olabilir.
* Verileri korumak ama yine de referans olarak göndermek için `const` ifadesi kullanılır. Bu argümanları sadece okunabilir yapar.
* Örnek kod:
```cpp
	#include <iostream>
	
	// Referans ile çağırma örneği
	void increment(int &num) {
	    num = num + 1; // num değişkeninin kendisi üzerinde işlem yapılır
	    std::cout << "Inside function: " << num << std::endl;
	}
	
	int main() {
	    int a = 5;
	    increment(a); // a değişkeninin kendisi fonksiyona geçirilir
	    std::cout << "Outside function: " << a << std::endl; // a değişkeninin değeri değişir
	
	    return 0;
	}
```
### `&` ve `*` arasındaki fark
- `f(int &a)`: Referans kullanarak değişkenin kendisi üzerinde işlem yapar. Kullanımı daha basit ve güvenlidir.
- `f(int *a)`: İşaretçi kullanarak değişkenin adresi üzerinde işlem yapar. Daha esnek ama daha karmaşıktır ve dikkatli kullanılmalıdır.
## Mixed parameter-lists
* Bir fonksiyona aynı anda hem value hem de referance gönderilebilir.
* Örnek:
```cpp
	void mixedCall(int &par1, int par2, double &par3);
```
# Overloading and Default Arguments
### Overloading
* Farklı parametreler kullanarak aynı isimde birden fazla fonksiyon ya da operatör tanımlamaktır.
* [[04.01 - Overloading]]
### Default Arguments
* Fonksiyonların parametrelerine default değerler atayabilirz. Ör: `int f(int a = 5, int b = 10);`. a ya da b parametreleri yerine bir argüman yollanmazsa bu default değerler kullanılır.
# Testing and Debugging Functions
### `assert` makrosu
* Bir condition kontrol eder. Eğer condition'dan true dönerse kod çalışmaya devam eder. Eğer false dönerse program kapanır bir hata kodu döner.
* Ör: 
```cpp
	#include <iostream>
	#include <cassert> // assert makrosu için gerekli
	
	int main() {
	    int x = 5;
	    int y = 10;
	
	    // x'in y'den küçük olduğunu kontrol et
	    assert(x < y);
	
	    std::cout << "Assertion passed, x is less than y." << std::endl;
	
	    // Yanlış bir ifade ile assert
	    assert(x > y); // Bu ifade yanlış olduğu için program burada durur
	
	    std::cout << "This line will not be executed." << std::endl;
	
	    return 0;
	}
```
### `assert` açma ve kapama
* Eğer `#include <cassert>` satırından önce `#define NDEBUG` ifadesini eklersek ve , assert fonksiyonları çalışmaz. Bu da bir programın deploy ve testing süreçlerinde kolaylıklar sağlar. 
### Stub
* Stub, yazılım geliştirme ve test süreçlerinde kullanılan bir tekniktir. Gerçek bir fonksiyon veya modülün yerine geçici olarak kullanılan basit bir versiyonudur. Stub'lar, özellikle henüz geliştirilmemiş veya erişilemeyen bileşenlerin yerine kullanılarak, sistemin geri kalanının test edilmesine olanak tanır.
- **Geçici**: Gerçek fonksiyon veya modül geliştirilene kadar kullanılır.
- **Basit**: Genellikle sadece temel işlevselliği sağlar ve karmaşık işlemler içermez.
- **Test Odaklı**: Test senaryolarında belirli koşulları simüle etmek için kullanılır.
* Örnek:
```cpp
	#include <iostream>
	
	// Gerçek fonksiyonun yerine kullanılacak stub fonksiyon
	int add(int a, int b) {
	    return a + b; // Basit bir toplama işlemi
	}
	
	// Test edilecek fonksiyon
	int calculateSum(int x, int y) {
	    // Gerçek fonksiyon yerine stub fonksiyon kullanılıyor
	    return add(x, y);
	}
	
	int main() {
	    int result = calculateSum(3, 4);
	    std::cout << "Result: " << result << std::endl; // Result: 7
	    return 0;
	}
```

Bu örnekte, `add` fonksiyonu bir stub olarak kullanılmıştır. `calculateSum` fonksiyonu, `add` fonksiyonunu çağırarak iki sayının toplamını hesaplar. Gerçek `add` fonksiyonu daha karmaşık olabilir, ancak test sürecinde basit bir stub kullanmak yeterlidir.

### Driver
* Var olan fonksiyonun doğru çalışıp çalışmadığını test eden ara fonksiyondur.
* Örnek: 
```cpp
	#include <iostream>
	
	// Test edilecek fonksiyon
	int multiply(int a, int b) {
	    return a * b;
	}
	
	// Driver fonksiyon
	void testMultiply() {
	    int x = 5;
	    int y = 10;
	    int result = multiply(x, y);
	    std::cout << "Result: " << result << std::endl; // Result: 50
	}
	
	int main() {
	    testMultiply(); // Driver fonksiyonunu çağır
	    return 0;
	}
```