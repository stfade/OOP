*Links*: [[00 - Index]]
*Date*: 09.12.2024
*Resources*: [name]()

---
# Introduction
Tipik geliştirme yaklaşımı şu şekildedir:
- Programları her şeyin planlandığı gibi gideceğini varsayarak yazmak.
- "Çekirdek" işlevselliği çalıştırmak.
- Daha sonra "istisnai" durumlarla ilgilenmek.

C++ istisna (exception) işleme olanakları:
- "İstisnai" durumları ele almak.
- Mekanizma, olağandışı bir durumu "sinyal" eder.
- Kodun başka bir yeri istisna ile "ilgilenir".
# Exception Handling Basics
Exception handling mekanizması, nadiren ve karmaşık durumlarda kullanılmalıdır. Büyük örnekleri öğretmek zor olabilir. Bu nedenle, genellikle exception handling kullanmayan basit örneklerle başlamak daha iyidir. Ancak, her zaman büyük resmi akılda tutmak önemlidir.

**Example:**
Hayal edin: İnsanlar nadiren sütü bitirir:
```cpp
#include <iostream>
using namespace std;

int main() {
    int donuts, milk;
    cout << "Enter number of donuts: ";
    cin >> donuts;
    cout << "Enter number of glasses of milk: ";
    cin >> milk;

    double dpg = donuts / static_cast<double>(milk);
    cout << donuts << " donuts.\n";
    cout << milk << " glasses of milk.\n";
    cout << "You have " << dpg << " donuts for each glass of milk.\n";

    return 0;
}
```
Bu temel kod, sütün hiç bitmeyeceğini varsayar.

Dikkat: Eğer süt yoksa, sıfıra bölme hatası oluşur! Program, sütün bitmesi gibi olası olmayan durumu göz önünde bulundurmalıdır. Basit bir if-else yapısı kullanılabilir:
```cpp
#include <iostream>
using namespace std;

int main() {
    int donuts, milk;
    cout << "Enter number of donuts: ";
    cin >> donuts;
    cout << "Enter number of glasses of milk: ";
    cin >> milk;

    if (milk <= 0) {
        cout << "Go buy some milk!\n";
    } else {
        double dpg = donuts / static_cast<double>(milk);
        cout << donuts << " donuts.\n";
        cout << milk << " glasses of milk.\n";
        cout << "You have " << dpg << " donuts for each glass of milk.\n";
    }

    return 0;
}
```
Dikkat: Burada exception-handling kullanılmamıştır.

Try ve catch anahtar kelimeleri arasındaki kod, sıradan versiyondaki kodla aynıdır, ancak if ifadesi daha basittir:
```cpp
#include <iostream>
using namespace std;

int main() {
    int donuts, milk;
    cout << "Enter number of donuts: ";
    cin >> donuts;
    cout << "Enter number of glasses of milk: ";
    cin >> milk;

    try {
        if (milk <= 0) {
            throw donuts;
        }
        double dpg = donuts / static_cast<double>(milk);
        cout << donuts << " donuts.\n";
        cout << milk << " glasses of milk.\n";
        cout << "You have " << dpg << " donuts for each glass of milk.\n";
    } catch (int e) {
        cout << "No milk available! You have " << e << " donuts. Go buy some milk!\n";
    }

    return 0;
}
```
Bu daha temiz bir koddur. Eğer "süt yoksa" exceptional bir durum oluşur ve bu durum catch anahtar kelimesinden sonra ele alınır.

Try bloğu "normal" durumu ele alır. Catch bloğu ise "exceptional" durumları ele alır. Bu, normal durumları exceptional durumlardan ayırır. Bu basit örnek için büyük bir mesele olmasa da, önemli bir kavramdır.

***Exception handling'in temel yöntemi try-throw-catch yapısıdır.***

## Try
```cpp
try {
    // Some_Code;
}
```
Bu blok, her şeyin sorunsuz gittiği temel algoritma kodunu içerir.

## Throw
Try bloğu içinde, olağandışı bir durum meydana geldiğinde:
```cpp
try {
    // Code_To_Try
    if (exceptional_happened) {
        throw donuts;
    }
    // More_Code
}
```
Throw anahtar kelimesi ve ardından exception türü gelir. Bu duruma "throwing an exception" denir.

## Catch 
Bir şey throw edildiğinde, kontrol akışı try bloğundan catch bloğuna geçer. C++'ta, try bloğu "çıkılır" ve kontrol catch bloğuna geçer. Catch bloğunun çalıştırılmasına "catching the exception" denir. Exception'lar mutlaka bir catch bloğunda "handled" edilmelidir.

```cpp
#include <iostream>
using namespace std;

int main() {
    int donuts, milk;
    cout << "Enter number of donuts: ";
    cin >> donuts;
    cout << "Enter number of glasses of milk: ";
    cin >> milk;

    try {
        if (milk <= 0) {
            throw donuts; // Throwing an exception
        }
        double dpg = donuts / static_cast<double>(milk);
        cout << donuts << " donuts.\n";
        cout << milk << " glasses of milk.\n";
        cout << "You have " << dpg << " donuts for each glass of milk.\n";
    } catch (int e) {
        // Catching the exception
        cout << "No milk available! You have " << e << " donuts. Go buy some milk!\n";
    }

    return 0;
}
```

Bu kodda, try bloğunda olağandışı bir durum meydana geldiğinde throw ile exception fırlatılır ve kontrol catch bloğuna geçer. Catch bloğu exception'ı yakalar ve işler.

Hatırlayın:
```cpp
catch(int e) {
    cout << e << " donuts, and no milk!\n";
    cout << "Go buy some milk.\n";
}
```
Bu, int parametreli bir fonksiyon tanımı gibi görünür! Fonksiyon olmasa da benzer şekilde çalışır. Throw, bir "function call" gibi davranır.

`throw` ifadesi, herhangi bir türdeki değeri fırlatabilir. Exception sınıfı, fırlatılacak bilgiler içeren nesneleri barındırır. Her olası istisnai durumu tanımlayan farklı türlere sahip olabilir. Yine de sadece bir sınıftır. Kullanım şekli nedeniyle "exception class" olarak adlandırılır.

## Exception class for the example
```cpp
class NoMilk
{
public:
	NoMilk() { }
	NoMilk(int howMany) : count(howMany) { }
	int getcount() const { return count; }
private:
	int count;
};
```

- `NoMilk` adında bir sınıf tanımlanmış.
- Bu sınıfın iki kurucusu (constructor) var: biri parametresiz, diğeri `int howMany` parametresi alıyor ve `count` üyesini bu parametre ile başlatıyor.
- `getcount` adında, `count` üyesini döndüren bir üye fonksiyonu var.
- `count` adında özel (private) bir üye değişkeni var.

```cpp
throw NoMilk(donuts);
```

- `NoMilk` sınıfının `int` parametreli kurucusunu çağırarak bir `NoMilk` nesnesi oluşturur ve bu nesneyi fırlatır (throw).

# Multiple Throws and Catches
`try` bloğu genellikle farklı türlerde herhangi bir sayıda istisna değeri fırlatabilir. Ancak, `throw` ifadesi `try` bloğunu sonlandırdığı için sadece bir istisna fırlatılır. Farklı türlerde istisnalar fırlatılabilir ve her `catch` bloğu sadece "bir tür" istisnayı yakalar. Bu nedenle, her `try` bloğunun ardından "tüm olası" istisnaları yakalamak için birçok `catch` bloğu yerleştirilmesi yaygındır.

## Catching
`catch` bloklarının sırası önemlidir. `try` bloğundan sonra `catch` blokları "sırayla" denenir ve ilk eşleşen blok istisnayı işler. Örneğin:

```cpp
catch (...) { }
```

Bu, "catch-all" veya "default" istisna işleyici olarak adlandırılır ve herhangi bir istisnayı yakalar. `catch-all` bloğunun, daha spesifik istisnaların ardından yerleştirildiğinden emin olunmalıdır, aksi takdirde diğer istisnalar asla yakalanmaz.

## Trivial Exception Classes
```cpp
class DivideByZero
{ }
```

- `DivideByZero` adında bir sınıf tanımlanmış.
- Bu sınıfın üye değişkenleri yok.
- Varsayılan kurucu dışında üye fonksiyonları yok.
- Sınıfın sadece adı var ve bu, exception handling için yeterli.
- Exception değeri ile ilgili herhangi bir bilgi taşımayabilir.
- Sadece `catch` bloğuna ulaşmak için kullanılır.
- `catch` bloğu parametresi atlanabilir. Örneğin:

```cpp
try {
    // Kod burada
} catch (DivideByZero) {
    // Exception handling burada
}
```

Bu şekilde, `DivideByZero` sınıfı sadece bir exception olduğunu belirtmek için kullanılır ve herhangi bir ek bilgi taşımaz.

# Throwing Exception in Function

Bir fonksiyon exception fırlatabilir. Çağıranlar farklı "tepkilere" sahip olabilir. Bazıları programı "sonlandırmak" isteyebilir, bazıları devam edebilir veya başka bir şey yapabilir. Bu nedenle, exception'ı çağıran fonksiyonun `try-catch` bloğunda "yakalamak" mantıklıdır. Çağrıyı `try` bloğunun içine yerleştirin ve `try` bloğundan sonra `catch` bloğunda işleyin.

Örneğin:

```cpp
void mightThrow() {
    // Exception fırlatabilir
}

void callerFunction() {
    try {
        mightThrow();
    } catch (const std::exception& e) {
        // Exception handling burada
    }
}
```

Bu şekilde, `mightThrow` fonksiyonu exception fırlatırsa, `callerFunction` içinde yakalanır ve uygun şekilde işlenir.

# Exception Specification
Exception yakalamayan fonksiyonlar, kullanıcıları exception fırlatabileceği konusunda "uyarmalıdır". Ancak bu exception'ları yakalamayacaklarını belirtmelidirler. Bu tür exception'lar listelenmelidir:

```cpp
double safeDivide(int top, int bottom) throw (DivideByZero);
```

Bu, "exception specification" veya "throw list" olarak adlandırılır. Hem deklarasyonda hem de tanımda bulunmalıdır. Listelenen tüm türler "normal" şekilde işlenir. Eğer throw listesi yoksa, tüm türler orada kabul edilir.

Örneğin:

```cpp
double safeDivide(int top, int bottom) throw (DivideByZero) {
    if (bottom == 0) {
        throw DivideByZero();
    }
    return static_cast<double>(top) / bottom;
}
```

Bu şekilde, `safeDivide` fonksiyonu `DivideByZero` exception'ı fırlatabileceğini belirtir, ancak bu exception'ı yakalamaz.

Eğer bir fonksiyonda throw listesinde olmayan bir exception fırlatılırsa:

- Derleme veya çalışma zamanı hatası oluşmaz.
- `unexpected()` fonksiyonu otomatik olarak çağrılır.
- Varsayılan davranış programı sonlandırmaktır.
- Bu davranış değiştirilebilir.
- Aynı sonuç, eğer bir `catch` bloğu bulunamazsa da geçerlidir.

Örneğin:

```cpp
double safeDivide(int top, int bottom) throw (DivideByZero) {
    if (bottom == 0) {
        throw DivideByZero();
    }
    return static_cast<double>(top) / bottom;
}

void unexpectedHandler() {
    std::cerr << "Unexpected exception caught!" << std::endl;
    std::terminate();
}

int main() {
    std::set_unexpected(unexpectedHandler);

    try {
        safeDivide(10, 0);
    } catch (...) {
        std::cerr << "Exception caught!" << std::endl;
    }

    return 0;
}
```

Bu örnekte, `safeDivide` fonksiyonu `DivideByZero` exception'ı fırlatırsa ve bu exception throw listesinde değilse, `unexpectedHandler` fonksiyonu çağrılır ve program sonlandırılır. Eğer bir `catch` bloğu bulunamazsa da aynı sonuç geçerlidir.

### Özetle:

```cpp
void someFunction() throw(DivideByZero, OtherException);
// DivideByZero veya OtherException türündeki exception'lar normal şekilde işlenir.
// Diğer tüm exception'lar unexpected() fonksiyonunu çağırır.

void someFunction() throw ();
// Boş exception listesi, tüm exception'lar unexpected() fonksiyonunu çağırır.

void someFunction();
// Tüm türlerdeki exception'lar normal şekilde işlenir.
```

- İlk fonksiyon, `DivideByZero` veya `OtherException` exception'larını normal şekilde işler. Diğer tüm exception'lar `unexpected()` fonksiyonunu çağırır.
- İkinci fonksiyon, boş exception listesi ile tanımlanmıştır. Bu, tüm exception'ların `unexpected()` fonksiyonunu çağıracağı anlamına gelir.
- Üçüncü fonksiyon, herhangi bir exception listesi belirtmez. Bu, tüm türlerdeki exception'ların normal şekilde işleneceği anlamına gelir.

# Derived Classes
Unutmayın: türetilmiş sınıf nesneleri aynı zamanda temel sınıfın nesneleridir.

Örneğin:

- `D`, `B` sınıfından türetilmiş bir sınıftır.
- Eğer `B`, exception specification'da belirtilmişse, `D` sınıfından fırlatılan nesneler de normal şekilde işlenecektir, çünkü `D` aynı zamanda `B` sınıfının bir nesnesidir.

Önemli not: Bu, otomatik tür dönüşümü yapmaz. Örneğin, `double` türü, `int` türünde bir exception fırlatmayı kapsamaz.

Örnek:

```cpp
class B {};
class D : public B {};

void someFunction() throw(B) {
    throw D(); // Bu, normal şekilde işlenecektir çünkü D, B'nin bir nesnesidir.
}

void anotherFunction() throw(double) {
    throw 5; // Bu, normal şekilde işlenmez çünkü int, double'a otomatik olarak dönüştürülmez.
}
```

Bu şekilde, `D` sınıfından fırlatılan nesneler `B` sınıfı olarak kabul edilir ve normal şekilde işlenir. Ancak, tür dönüşümü otomatik olarak yapılmaz, bu yüzden `double` türü bir exception listesi `int` türünde bir exception'ı kapsamaz.

# unexpected()

Varsayılan olarak, bir exception yakalanmadığında program sonlandırılır. Bu davranışı değiştirmek için özel `include` dosyalarına veya `using` direktiflerine gerek yoktur ve genellikle bu varsayılan davranışı yeniden tanımlamaya ihtiyaç duyulmaz. Ancak, isterseniz `set_unexpected` fonksiyonunu kullanarak bu davranışı değiştirebilirsiniz. Bu fonksiyon, beklenmeyen bir exception fırlatıldığında çağrılacak özel bir fonksiyon tanımlamanıza olanak tanır. Detaylar için derleyici kılavuzuna veya ileri düzey kaynaklara başvurabilirsiniz.

Örneğin, aşağıdaki kodda `myUnexpected` adında bir fonksiyon tanımlanmış ve `set_unexpected` ile bu fonksiyon beklenmeyen exception'lar için işleyici olarak atanmıştır. Eğer bir exception fırlatılır ve yakalanmazsa, `myUnexpected` fonksiyonu çağrılır ve program sonlandırılır:

```cpp
#include <exception>

#include <iostream>


void myUnexpected() {
    std::cerr << "Beklenmeyen bir exception yakalandı!" << std::endl;
    std::terminate();
}

void testFunction() throw(int) {
    throw 'a'; // Bu, throw listesinde olmadığı için unexpected() fonksiyonunu çağırır.
}

int main() {
    std::set_unexpected(myUnexpected);

    try {
        testFunction();
    } catch (int) {
        std::cerr << "int türünde bir exception yakalandı!" << std::endl;
    }

    return 0;
}
```

Bu şekilde, beklenmeyen exception'lar için özel bir işleyici tanımlayarak programın davranışını kontrol edebilirsiniz.

# When to Throw Exceptions

Genellikle, `throw` ve `catch` ifadelerini ayrı fonksiyonlarda kullanmak yaygındır. Bu, kodun daha düzenli ve okunabilir olmasını sağlar. İşte bu yaklaşımı gösteren bir örnek:

### Throwing Function

`throw` ifadelerini fonksiyon tanımına dahil edin ve exception'ları `throw` listesinde belirtin. Hem deklarasyonda hem de tanımda bu listeyi ekleyin.

```cpp
// header.h
#ifndef HEADER_H
#define HEADER_H

class DivideByZero {};

void safeDivide(int a, int b) throw(DivideByZero);

#endif // HEADER_H
```

```cpp
// throwing.cpp
#include "header.h"

void safeDivide(int a, int b) throw(DivideByZero) {
    if (b == 0) {
        throw DivideByZero();
    }
    std::cout << "Sonuç: " << a / b << std::endl;
}
```

### Catching Function

Exception'ları yakalayan farklı bir fonksiyon yazın. Bu fonksiyon, belki de farklı bir dosyada olabilir.

```cpp
// catching.cpp
#include <iostream>
#include "header.h"

void myUnexpected() {
    std::cerr << "Beklenmeyen bir exception yakalandı!" << std::endl;
    std::terminate();
}

int main() {
    std::set_unexpected(myUnexpected);

    try {
        safeDivide(10, 0); // Bu, DivideByZero exception'ını fırlatır.
    } catch (const DivideByZero&) {
        std::cerr << "DivideByZero exception yakalandı!" << std::endl;
    }

    return 0;
}
```

### Açıklama

1. `header.h` dosyasında `DivideByZero` exception sınıfı ve `safeDivide` fonksiyonunun deklarasyonu bulunur.
2. `throwing.cpp` dosyasında `safeDivide` fonksiyonunun tanımı bulunur. Bu fonksiyon, `DivideByZero` exception'ını fırlatabilir.
3. `catching.cpp` dosyasında `main` fonksiyonu bulunur. Bu fonksiyon, `safeDivide` fonksiyonunu çağırır ve `DivideByZero` exception'ını yakalar.
4. `myUnexpected` fonksiyonu, beklenmeyen exception'lar için işleyici olarak tanımlanmıştır.

Bu şekilde, `throw` ve `catch` ifadelerini ayrı fonksiyonlarda ve dosyalarda kullanarak kodunuzu daha düzenli ve okunabilir hale getirebilirsiniz.

# Preferred throw-catch Triad
`functionA` fonksiyonu gerektiğinde `MyException` exception'ını fırlatır. İşte bu fonksiyonun nasıl tanımlanacağını ve kullanılacağını gösteren bir örnek:

### Exception Sınıfı ve Fonksiyon Deklarasyonu

Öncelikle, `MyException` sınıfını ve `functionA` fonksiyonunu tanımlayalım.

```cpp


//

 header.h
#ifndef HEADER_H
#define HEADER_H

class MyException {
public:
    MyException(const char* message) : msg(message) {}
    const char* what() const { return msg; }
private:
    const char* msg;
};

void functionA() throw (MyException);

#endif // HEADER_H
```

### Fonksiyon Tanımı

`functionA` fonksiyonunun tanımını yapalım. Bu fonksiyon gerektiğinde `MyException` exception'ını fırlatır.

```cpp
// functionA.cpp
#include "header.h"

void functionA() throw (MyException) {
    // Bazı işlemler
    bool errorOccurred = true; // Örnek hata durumu
    if (errorOccurred) {
        throw MyException("Bir hata oluştu!");
    }
    // Diğer işlemler
}
```

### Exception Yakalama

`functionA` fonksiyonunu çağıran ve exception'ı yakalayan bir fonksiyon yazalım.

```cpp
// main.cpp
#include <iostream>
#include "header.h"

void myUnexpected() {
    std::cerr << "Beklenmeyen bir exception yakalandı!" << std::endl;
    std::terminate();
}

int main() {
    std::set_unexpected(myUnexpected);

    try {
        functionA();
    } catch (const MyException& e) {
        std::cerr << "MyException yakalandı: " << e.what() << std::endl;
    }

    return 0;
}
```

### Açıklama

1. `header.h` dosyasında `MyException` sınıfı ve `functionA` fonksiyonunun deklarasyonu bulunur.
2. `functionA.cpp` dosyasında `functionA` fonksiyonunun tanımı bulunur. Bu fonksiyon, gerektiğinde `MyException` exception'ını fırlatır.

Bu şekilde, `functionA` fonksiyonu gerektiğinde `MyException` exception'ını fırlatır ve `main` fonksiyonu bu exception'ı yakalar ve işler.


# Uncaught Exceptions
Her fırlatılan exception yakalanmalıdır. Eğer yakalanmazsa, program sonlanır ve `terminate()` fonksiyonu çağrılır. Fonksiyonlar için, eğer exception `throw` listesinde değilse, `unexpected()` fonksiyonu çağrılır ve bu da `terminate()` fonksiyonunu çağırır. Sonuç olarak, program yine sonlanır.

Bu durumu daha iyi anlamak için bir örnek üzerinden gidelim:
### Exception Sınıfı ve Fonksiyon Deklarasyonu

Öncelikle, `MyException` sınıfını ve `functionA` fonksiyonunu tanımlayalım.

```cpp
// header.h
#ifndef HEADER_H
#define HEADER_H

class MyException {
public:
    MyException(const char* message) : msg(message) {}
    const char* what() const { return msg; }
private:
    const char* msg;
};

void functionA() throw (MyException);

#endif // HEADER_H
```

### Fonksiyon Tanımı

`functionA` fonksiyonunun tanımını yapalım. Bu fonksiyon gerektiğinde `MyException` exception'ını fırlatır.

```cpp
// functionA.cpp
#include "header.h"

void functionA() throw (MyException) {
    // Bazı işlemler
    bool errorOccurred = true; // Örnek hata durumu
    if (errorOccurred) {
        throw MyException("Bir hata oluştu!");
    }
    // Diğer işlemler
}
```

### Exception Yakalama

`functionA` fonksiyonunu çağıran ve exception'ı yakalayan `functionB` fonksiyonunu yazalım.

```cpp
// functionB.cpp
#include "header.h"
#include <iostream>

void functionB() {
    try {
        // Bazı işlemler
        functionA();
        // Diğer işlemler
    } catch (const MyException& e) {
        // Exception'ı işleme
        std::cerr << "MyException yakalandı: " << e.what() << std::endl;
    }
}
```

### Main Fonksiyonu

Son olarak, `functionB` fonksiyonunu çağıran `main` fonksiyonunu yazalım.

```cpp
// main.cpp
#include "header.h"

int main() {
    functionB();
    return 0;
}
```

### Açıklama

1. `header.h` dosyasında `MyException` sınıfı ve `functionA` fonksiyonunun deklarasyonu bulunur.
2. `functionA.cpp` dosyasında `functionA` fonksiyonunun tanımı bulunur. Bu fonksiyon, gerektiğinde `MyException` exception'ını fırlatır.
3. `functionB.cpp` dosyasında `functionA` fonksiyonunu çağıran ve `MyException` exception'ını yakalayan `functionB` fonksiyonu bulunur.
4. main.cpp dosyasında `functionB` fonksiyonunu çağıran `main` fonksiyonu bulunur.

Eğer `functionA` içinde `MyException` dışında bir exception fırlatılırsa, `unexpected()` fonksiyonu çağrılır ve bu da `terminate()` fonksiyonunu çağırarak programı sonlandırır. Bu nedenle, her fırlatılan exception'ı yakalamak önemlidir.

# Overuse of Exceptions
Exceptions, kontrol akışını değiştirir ve eski "goto" yapısına benzer şekilde "sınırsız" bir kontrol akışı sağlar. Bu nedenle, exception'lar dikkatli ve sınırlı bir şekilde kullanılmalıdır. İyi bir kural olarak, bir "throw" ifadesi kullanmak istediğinizde, programı throw kullanmadan nasıl yazabileceğinizi düşünün. Eğer alternatif bir çözüm makul ise, bu alternatifi tercih edin.

### Örnek
Aşağıda, exception kullanımı ve alternatif bir çözüm gösterilmektedir.
#### Exception Kullanımı
```cpp
#include <iostream>
#include <exception>

class MyException : public std::exception {
public:
    const char* what() const noexcept override {
        return "Bir hata oluştu!";
    }
};

void functionA(int value) {
    if (value < 0) {
        throw MyException();
    }
    std::cout << "Değer: " << value << std::endl;
}

int main() {
    try {
        functionA(-1);
    } catch (const MyException& e) {
        std::cerr << "Exception yakalandı: " << e.what() << std::endl;
    }
    return 0;
}
```

Bu örnekte, `functionA` fonksiyonu negatif bir değer aldığında `MyException` exception'ını fırlatır ve `main` fonksiyonu bu exception'ı yakalar.

#### Alternatif Çözüm

Exception kullanmadan aynı durumu ele alalım:

```cpp
#include <iostream>

bool functionA(int value, std::string& errorMessage) {
    if (value < 0) {
        errorMessage = "Bir hata oluştu!";
        return false;
    }
    std::cout << "Değer: " << value << std::endl;
    return true;
}

int main() {
    std::string errorMessage;
    if (!functionA(-1, errorMessage)) {
        std::cerr << "Hata: " << errorMessage << std::endl;
    }
    return 0;
}
```

Bu alternatif çözümde, `functionA` fonksiyonu bir hata mesajı döndürür ve `main` fonksiyonu bu mesajı kontrol eder. Bu yaklaşım, exception kullanmadan hataları ele alır ve kontrol akışını daha belirgin hale getirir.
### Sonuç

Exception'lar güçlü bir araçtır, ancak dikkatli kullanılmalıdır. Eğer exception kullanmadan makul bir alternatif çözüm bulabiliyorsanız, bu alternatifi tercih etmek genellikle daha iyidir. Bu, kodun okunabilirliğini ve bakımını kolaylaştırır.

# Exception Class Hierarchies
`DivideByZero` sınıfının `ArithmeticError` exception sınıfından türetildiği bir durumu düşünelim. Bu durumda, `ArithmeticError` için yazılmış tüm `catch` blokları `DivideByZero` exception'larını da yakalayacaktır. Ayrıca, `ArithmeticError` `throw` listesinde belirtilmişse, `DivideByZero` da bu listede kabul edilir.

### Örnek
Aşağıda, `ArithmeticError` ve `DivideByZero` sınıflarını tanımlayan ve bu sınıfları kullanan bir örnek verilmiştir.
#### Exception Sınıfları ve Fonksiyon Deklarasyonu

Öncelikle, `ArithmeticError` ve `DivideByZero` sınıflarını ve `functionA` fonksiyonunu tanımlayalım.

```cpp
// header.h
#ifndef HEADER_H
#define HEADER_H

class ArithmeticError : public std::exception {
public:
    const char* what() const noexcept override {
        return "Aritmetik hata!";
    }
};

class DivideByZero : public ArithmeticError {
public:
    const char* what() const noexcept override {
        return "Sıfıra bölme hatası!";
    }
};

void functionA() throw (ArithmeticError);

#endif // HEADER_H
```

#### Fonksiyon Tanımı

`functionA` fonksiyonunun tanımını yapalım. Bu fonksiyon gerektiğinde `DivideByZero` exception'ını fırlatır.

```cpp
// functionA.cpp
#include "header.h"

void functionA() throw (ArithmeticError) {
    // Bazı işlemler
    bool errorOccurred = true; // Örnek hata durumu
    if (errorOccurred) {
        throw DivideByZero();
    }
    // Diğer işlemler
}
```

#### Exception Yakalama

`functionA` fonksiyonunu çağıran ve exception'ı yakalayan `functionB` fonksiyonunu yazalım.

```cpp
// functionB.cpp
#include "header.h"
#include <iostream>

void functionB() {
    try {
        // Bazı işlemler
        functionA();
        // Diğer işlemler
    } catch (const ArithmeticError& e) {
        // ArithmeticError ve türevlerini işleme
        std::cerr << "ArithmeticError yakalandı: " << e.what() << std::endl;
    }
}
```

#### Main Fonksiyonu

Son olarak, `functionB` fonksiyonunu çağıran `main` fonksiyonunu yazalım.

```cpp
// main.cpp
#include "header.h"

int main() {
    functionB();
    return 0;
}
```

### Açıklama

1. `header.h` dosyasında `ArithmeticError` ve `DivideByZero` exception sınıfları ile `functionA` fonksiyonunun deklarasyonu bulunur.
2. `functionA.cpp` dosyasında `functionA` fonksiyonunun tanımı bulunur. Bu fonksiyon, gerektiğinde `DivideByZero` exception'ını fırlatır.
3. `functionB.cpp` dosyasında `functionA` fonksiyonunu çağıran ve `ArithmeticError` exception'ını yakalayan `functionB` fonksiyonu bulunur. `ArithmeticError` exception'ı `DivideByZero` exception'larını da yakalar.
4. main.cpp dosyasında `functionB` fonksiyonunu çağıran `main` fonksiyonu bulunur.

Bu şekilde, `DivideByZero` sınıfı `ArithmeticError` sınıfından türetildiği için, `ArithmeticError` için yazılmış `catch` blokları `DivideByZero` exception'larını da yakalar. Ayrıca, `ArithmeticError` `throw` listesinde belirtilmişse, `DivideByZero` da bu listede kabul edilir.

# Testing Available Memory
`new` operatörü yeterli bellek olmadığında `bad_alloc` exception'ını fırlatır. Bu exception'ı yakalamak için `try-catch` bloğu kullanabilirsiniz. `bad_alloc` exception'ı `<new>` kütüphanesinde ve `std` isim alanında bulunur.

### Örnek

Aşağıda, `new` operatörünün `bad_alloc` exception'ı fırlattığı ve bu exception'ı yakalayan bir örnek verilmiştir:

```cpp
#include <iostream>
#include <new> // std::bad_alloc için gerekli

class Node {
    // Node sınıfı tanımı
};

int main() {
    try {
        Node* pointer = new Node; // Bellek tahsisi
    } catch (const std::bad_alloc& e) {
        std::cerr << "Bellek yetersiz: " << e.what() << std::endl;
        // Burada başka işlemler de yapabilirsiniz
    }

    return 0;
}
```

### Açıklama

1. `<new>` kütüphanesi `std::bad_alloc` exception'ını kullanmak için dahil edilmiştir.
2. `Node` sınıfı tanımlanmıştır (örnek olarak boş bırakılmıştır).
3. `main` fonksiyonunda, `new` operatörü kullanılarak bir `Node` nesnesi için bellek tahsis edilmeye çalışılır.
4. Eğer yeterli bellek yoksa, `new` operatörü `std::bad_alloc` exception'ını fırlatır.
5. `catch` bloğunda, `std::bad_alloc` exception'ı yakalanır ve bir hata mesajı yazdırılır. Ayrıca, burada başka işlemler de yapabilirsiniz.

Bu şekilde, `new` operatörü tarafından fırlatılan `bad_alloc` exception'ını yakalayarak bellek yetersizliği durumunda uygun işlemleri gerçekleştirebilirsiniz.

# Rethrowing an Exception
Bir `catch` bloğu içinde exception fırlatmak yasaldır ve genellikle nadir durumlarda kullanılır. Bu, exception'ı "daha yukarıdaki" bir `catch` bloğuna iletmek için yapılır. Aynı exception'ı yeniden fırlatabilir veya yeni bir exception fırlatabilirsiniz.

### Örnek

Aşağıda, bir `catch` bloğu içinde exception fırlatmayı ve yeniden fırlatmayı gösteren bir örnek verilmiştir:

```cpp
#include <iostream>
#include <exception>

class MyException : public std::exception {
public:
    const char* what() const noexcept override {
        return "MyException oluştu!";
    }
};

class

 Another

Exception : public std::exception {
public:
    const char* what() const noexcept override {
        return "AnotherException oluştu!";
    }
};

void functionA() {
    throw MyException();
}

void functionB() {
    try {
        functionA();
    } catch (const MyException& e) {
        std::cerr << "functionB içinde yakalandı: " << e.what() << std::endl;
        throw; // Aynı exception'ı yeniden fırlat
    }
}

int main() {
    try {
        functionB();
    } catch (const MyException& e) {
        std::cerr << "main içinde yakalandı: " << e.what() << std::endl;
    } catch (const AnotherException& e) {
        std::cerr << "main içinde yakalandı: " << e.what() << std::endl;
    }

    return 0;
}
```

### Açıklama

1. `MyException` ve `AnotherException` adında iki exception sınıfı tanımlanmıştır.
2. `functionA` fonksiyonu `MyException` exception'ını fırlatır.
3. `functionB` fonksiyonu `functionA` fonksiyonunu çağırır ve `MyException` exception'ını yakalar. Bu exception'ı yakaladıktan sonra, aynı exception'ı yeniden fırlatır (`throw;`).
4. `main` fonksiyonu `functionB` fonksiyonunu çağırır ve `MyException` exception'ını yakalar. Ayrıca, `AnotherException` exception'ını yakalamak için de bir `catch` bloğu bulunmaktadır.

Bu örnekte, `functionA` `MyException` exception'ını fırlatır ve `functionB` bu exception'ı yakalar. `functionB` içinde aynı exception yeniden fırlatılır ve `main` fonksiyonu bu exception'ı yakalar. Bu, exception'ların daha yukarıdaki `catch` bloklarına iletilmesini sağlar.

Ayrıca, yeni bir exception fırlatmak isterseniz, `throw new AnotherException();` ifadesini kullanabilirsiniz:

```cpp
void functionB() {
    try {
        functionA();
    } catch (const MyException& e) {
        std::cerr << "functionB içinde yakalandı: " << e.what() << std::endl;
        throw AnotherException(); // Yeni bir exception fırlat
    }
}
```

Bu durumda, `functionB` içinde `MyException` yakalandığında, `AnotherException` fırlatılır ve `main` fonksiyonunda yakalanır.

# Özet Kod
```cpp
#include <iostream>
#include <exception>
#include <new> // std::bad_alloc için gerekli

// Exception sınıfları
class ArithmeticError : public std::exception {
public:
    const char* what() const noexcept override {
        return "Aritmetik hata!";
    }
};

class DivideByZero : public ArithmeticError {
public:
    const char* what() const noexcept override {
        return "Sıfıra bölme hatası!";
    }
};

class MyException : public std::exception {
public:
    MyException(const char* message) : msg(message) {}
    const char* what() const noexcept override {
        return msg;
    }
private:
    const char* msg;
};

// Fonksiyon deklarasyonları
void functionA() throw (ArithmeticError, MyException);
void functionB();
double safeDivide(int top, int bottom) throw (DivideByZero);

// Fonksiyon tanımları
void functionA() throw (ArithmeticError, MyException) {
    // Örnek hata durumu
    bool errorOccurred = true;
    if (errorOccurred) {
        throw MyException("Bir hata oluştu!"); // MyException fırlat
    }
}

void functionB() {
    try {
        functionA(); // functionA çağır
    } catch (const MyException& e) {
        std::cerr << "functionB içinde yakalandı: " << e.what() << std::endl;
        throw; // Aynı exception'ı yeniden fırlat
    }
}

double safeDivide(int top, int bottom) throw (DivideByZero) {
    if (bottom == 0) {
        throw DivideByZero(); // DivideByZero exception'ı fırlat
    }
    return static_cast<double>(top) / bottom; // Bölme işlemi
}

void myUnexpected() {
    std::cerr << "Beklenmeyen bir exception yakalandı!" << std::endl;
    std::terminate(); // Programı sonlandır
}

int main() {
    std::set_unexpected(myUnexpected); // Beklenmeyen exception işleyicisini ayarla

    // Bellek tahsisi ve bad_alloc yakalama
    try {
        int* largeArray = new int[1000000000]; // Büyük bir bellek tahsisi
    } catch (const std::bad_alloc& e) {
        std::cerr << "Bellek yetersiz: " << e.what() << std::endl; // Bellek yetersizliği mesajı
    }

    // DivideByZero exception'ı yakalama
    try {
        double result = safeDivide(10, 0); // safeDivide fonksiyonunu çağır
        std::cout << "Sonuç: " << result << std::endl;
    } catch (const DivideByZero& e) {
        std::cerr << "DivideByZero yakalandı: " << e.what() << std::endl; // DivideByZero exception'ı yakala
    }

    // functionB çağrısı ve exception yakalama
    try {
        functionB(); // functionB fonksiyonunu çağır
    } catch (const MyException& e) {
        std::cerr << "main içinde yakalandı: " << e.what() << std::endl; // MyException yakala
    } catch (const ArithmeticError& e) {
        std::cerr << "main içinde yakalandı: " << e.what() << std::endl; // ArithmeticError yakala
    }

    return 0;
}
```

### Açıklama

1. **Exception Sınıfları**: `ArithmeticError`, `DivideByZero`, ve `MyException` sınıfları tanımlanmıştır.
   - `ArithmeticError`: Genel aritmetik hataları temsil eder.
   - `DivideByZero`: `ArithmeticError` sınıfından türetilmiştir ve sıfıra bölme hatalarını temsil eder.
   - `MyException`: Genel bir hata mesajı içeren özel bir exception sınıfıdır.

2. **Fonksiyon Deklarasyonları**: `functionA`, `functionB`, ve `safeDivide` fonksiyonları tanımlanmıştır.
   - `functionA`: `ArithmeticError` ve `MyException` exception'larını fırlatabilir.
   - `functionB`: `functionA` fonksiyonunu çağırır ve exception'ları yakalar.
   - `safeDivide`: `DivideByZero` exception'ını fırlatabilir.

3. **Fonksiyon Tanımları**:
   - `functionA`: Örnek bir hata durumu oluşturur ve `MyException` fırlatır.
   - `functionB`: `functionA` fonksiyonunu çağırır ve `MyException` exception'ını yakalar, ardından aynı exception'ı yeniden fırlatır.
   - `safeDivide`: Sıfıra bölme durumunu kontrol eder ve `DivideByZero` exception'ı fırlatır.

4. **`myUnexpected` Fonksiyonu**: Beklenmeyen exception'lar için işleyici olarak tanımlanmıştır. Beklenmeyen bir exception yakalandığında, hata mesajı yazdırır ve programı sonlandırır.

5. **`main` Fonksiyonu**:
   - Bellek tahsisi yapar ve `bad_alloc` exception'ını yakalar.
   - `safeDivide` fonksiyonunu çağırır ve `DivideByZero` exception'ını yakalar.
   - `functionB` fonksiyonunu çağırır ve `MyException` ile `ArithmeticError` exception'larını yakalar.

Bu kod, exception handling'in temel kavramlarını ve kullanımını kapsamlı bir şekilde göstermektedir.