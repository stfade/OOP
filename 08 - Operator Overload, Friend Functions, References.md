*Links*: [[00 - Index|Index]]
*Date*: 29.10.2024
*Resources*: [name]()

---
# Basic Operator Overloading
- Operatörler (+, -, %, vb.) aslında fonksiyonlardır.
- Farklı bir sözdizimi ile "çağrılırlar".
- Örneğin, `x + 7` ifadesinde "+" bir ikili operatördür. x ile 7 operand olarak kullanılır. Bunu şu şekilde düşünebilirsiniz: `+(x, 7)`. Burada "+" fonksiyonun adıdır. x ile 7 argümanlardır. "+" fonksiyonu, argümanlarının "toplamını" döner.
- İnsanlar olarak bu gösterimi beğeniriz.
- Yerleşik operatörler (örn. +, -, =, %,  /, \*) C++'ın yerleşik türleri için zaten çalışır.
- Bu operatörler standart "binary" gösterimde kullanılır.
- Biz bu operatörleri overload edebiliriz!
- Bu sayede operatörleri KENDİ türlerimizle çalışacak şekilde ayarlayabiliriz.
- Operatörleri her zaman benzer "eylemler" ile aşırı yükleyin!
- Örnek Bildirim:
    ```cpp
	    const Money operator +(const Money& amount1, const Money& amount2);
    ```
    
- Bu bildirim, + operatörünü Money türündeki operandlar için aşırı yükler.
- Verimlilik için sabit referans (constant reference) parametreler kullanır.
- Döndürülen değer Money türündedir.
- Bu, "Money" nesnelerinin toplanmasına olanak tanır.
- Dikkat: Overload edilen "+" bir üye fonksiyon değildir. Sadece "kendi" türünüze özgü "toplama" işlemini gerçekleştirir.
- Eşitlik operatörü, `==` nesnelerinin karşılaştırılmasını sağlar.
- Bildirim:
    ```cpp
	    bool operator ==(const Money& amount1, const Money& amount2);
    ```
    
- Bu fonksiyon, true/false eşitliği için bool türünde bir değer döner.
- Yine, bu fonksiyon bir üye fonksiyon değildir (tıpkı "+" aşırı yüklemesi gibi).
### Constructors Returning Objects
- **Constructor** bir "void" fonksiyon değildir. **Özel** bir fonksiyondur ve özel özelliklere sahiptir. 
- **Değer döndürebilir**!
- "+" aşırı yüklemesindeki return ifadesini hatırlayın:
    ```cpp
	    return Money(finalDollars, finalCents);
    ```
    
- Bu ifade, Money sınıfının bir **çağrımını** döner! Yani constructor aslında bir **nesne döndürür**!
- Buna **anonim nesne** denir.

**Anonim Nesne**: Fonksiyon, yeni oluşturulan `Money` nesnesini döndürür. Bu nesne anonimdir çünkü bir değişkene atanmaz, doğrudan döndürülür.
### Returning by const Value
- `+` operatör aşırı yüklemesini tekrar düşünelim:
    ```cpp
	    const Money operator +(const Money& amount1, const Money& amount2);
    ```
    
- Bu, bir "sabit nesne" döndürür.
- Sabit olmayan bir nesnenin döndürülmesinin etkisini düşünelim:
    - Döndürülen nesne değiştirilebilir olur.
    - Bu, istemeden nesnenin değiştirilmesine yol açabilir.
    - Kodun güvenliğini ve kararlılığını azaltır.
    - Sabit nesne döndürmek, bu tür hataların önüne geçer ve kodun güvenliğini artırır.
### Returning by non-const Value
- m1 + m2 ifadesi tarafından döndürülen nesne üzerinde üye fonksiyonları çağırabiliriz:
    ```cpp
    (m1 + m2).output();  // Yasal, değil mi?
    ```
    Sorun yok: bu, herhangi bir şeyi değiştirmez.
- Ancak:
    ```cpp
    (m1 + m2).input();  // Yasal!
    ```
- PROBLEM! Yasal, ama DEĞİŞTİRİYOR!
- Bu, "anonim" nesnenin değiştirilmesine izin verir! Bu duruma izin veremeyiz! Bu yüzden döndürülen nesneyi const olarak tanımlarız.
## Unary Operators
- C++'ta tekli (unary) operatörler vardır. Tek bir operand alacak şekilde tanımlanırlar.
- Örneğin, - (negatifleme) operatörü:
    ```cpp
    x = -y;  // x'i y'nin negatifine eşitler
    ```
    
- Diğer tekli operatörler:
    - `++` (arttırma)
    - `--` (azaltma)
- Tekli operatörler de overload edilebilir.
- Tekli "-" operatörü overload edilmiş olarak sınıfın dışında bildirilir ve sadece bir argüman alır, bu da onu tek operandlı (unary) yapar, ancak aynı operatör iki operand/argüman (binary) için de aşırı yüklenmelidir.
- Örnek:
	```cpp
		class Money {
		public:
		    // Unary operator overload
		    const Money operator -(const Money& amount) {
		        return Money(-amount.dollars, -amount.cents);
		    }
		
		    // Binary operator overload
		    const Money operator -(const Money& amount1, const Money& amount2) {
		        int totalCents1 = amount1.dollars * 100 + amount1.cents;
		        int totalCents2 = amount2.dollars * 100 + amount2.cents;
		        int finalCents = totalCents1 - totalCents2;
		        return Money(finalCents / 100, finalCents % 100);
		    }
		
		private:
		    int dollars;
		    int cents;
		};
	```

Bu örnek, `Money` sınıfı için hem tekli (`-amount`) hem de ikili (`amount1 - amount2`) "-" operatörlerinin aşırı yüklenmesini göstermektedir.

**Built-in Türler İçin Bilinen Operasyon**: Unary "-" operatörü, built-in türler (örneğin, `int`, `double`) için zaten tanımlıdır. Bu operatör, bir sayının negatifini alır. Bu fonksiyon, aynı işlemi `Money` sınıfı için tanımlar.
- Örnek Kullanım: 
	```cpp
		Money m1(10, 50); // 10 dolar 50 cent
		Money m2 = -m1;  // -10 dolar -50 cent
	```

Bu örnekte, `m1` nesnesine unary "-" operatörü uygulanır ve `m2` nesnesi, `m1`'in negatif değerlerine sahip yeni bir `Money` nesnesi olur.
## As Member Functions
- Önceki örneklerde operatör aşırı yüklemeleri bağımsız fonksiyonlar olarak tanımlandı. Bunlar bir sınıfın dışında tanımlandı.
- Operatör aşırı yüklemelerini "üye operatör" olarak da aşırı yükleyebiliriz. Bu, diğer üye fonksiyonlar gibi kabul edilir.
- Operatör bir üye fonksiyon olduğunda:
    - Sadece BİR parametre alır, iki değil!
    - Çağıran nesne ilk parametre olarak hizmet eder.
- Örnek:
	```cpp
		class Money {
		private:
		    int dollars;
		    int cents;
		
		public:
		    // Constructor
		    Money(int d = 0, int c = 0) : dollars(d), cents(c) {}
		
		    // Unary "-" operator overload as a member function
		    Money operator-() const {
		        return Money(-dollars, -cents);
		    }
		
		    // Binary "-" operator overload as a member function
		    Money operator-(const Money& other) const {
		        int totalCents1 = dollars * 100 + cents;
		        int totalCents2 = other.dollars * 100 + other.cents;
		        int diffCents = totalCents1 - totalCents2;
		
		        int resultDollars = diffCents / 100;
		        int resultCents = diffCents % 100;
		
		        return Money(resultDollars, resultCents);
		    }
		
		    // Output function for displaying the amount
		    void output() const {
		        std::cout << "$" << dollars << "." << (cents < 10 ? "0" : "") << cents << std::endl;
		    }
		};
	```
### Member Function Operatörleri Kullanma
Eğer `+` operatörü bir sınıf üyesi olarak aşırı yüklenirse, çağıran nesne (bu durumda `cost`) ilk parametre olarak kabul edilir ve fonksiyon yalnızca bir parametre alır (bu durumda `tax`). Bu, `total = cost + tax;` ifadesinin aslında `total = cost.operator+(tax);` olarak düşünülebileceği anlamına gelir.
```cpp
	int main() {
	    Money cost(1, 50), tax(0, 15), total;
	    
	    // Binary "+" operator
	    total = cost + tax; // -> total = cost.operator+(tax); ile aynı
	    total.output(); // Displays $1.65
	    
	    return 0;
	}
```
### const Functions
- `const` fonksiyonlar, sınıf üye verilerini değiştirmelerine izin vermez.
- `const` nesneler SADECE `const` üye fonksiyonları çağırabilir.
- İyi stil şunu gerektirir:
    - Verileri DEĞİŞTİRMEYECEK herhangi bir üye fonksiyon `const` yapılmalıdır.
- `const` anahtar kelimesi fonksiyon bildirimi ve başlığından sonra kullanılmalıdır.
    ```cpp
	    class MyClass {
	    public:
	        void myFunction() const;  // const üye fonksiyon bildirimi
	    private:
	        int myData;
	    };
    ```
- **Neden `const` Üye Fonksiyonlar Kullanılır?**
	1. **Veri Bütünlüğü**: `const` üye fonksiyonlar, sınıfın üye verilerini değiştirmeyeceğini garanti eder. Bu, veri bütünlüğünü korur.
	2. **`const` Nesneler**: `const` olarak tanımlanan nesneler, yalnızca `const` üye fonksiyonları çağırabilir. Bu, `const` nesnelerin yanlışlıkla değiştirilmesini önler.
	3. **Kod Stili ve Güvenilirlik**: İyi bir kod stili, değişiklik yapmayan üye fonksiyonların `const` olarak işaretlenmesini gerektirir. Bu, kodun daha okunabilir ve güvenilir olmasını sağlar.
- Overload edilmiş operatörler de const olarak tanımlanabilir. Ör:
```cpp
	class Money {
	private:
		int dollars;
		int cents;
	
	public:
		// Constructor
		Money(int d = 0, int c = 0) : dollars(d), cents(c) {}
	
		// "+" operator overload as a member function
		const Money operator+(const Money& amount) const {
			int totalCents1 = dollars * 100 + cents;
			int totalCents2 = amount.dollars * 100 + amount.cents;
			int sumCents = totalCents1 + totalCents2;
	
			int resultDollars = sumCents / 100;
			int resultCents = sumCents % 100;
	
			return Money(resultDollars, resultCents);
		}
	
		// Unary "-" operator overload as a member function
		const Money operator-() const {
			return Money(-dollars, -cents);
		}
	
		// Output function for displaying the amount
		void output() const {
			std::cout << "$" << dollars << "." << (cents < 10 ? "0" : "") << cents << std::endl;
		}
	};
```
**Çağırma:**
```cpp
	int main() {
	    const Money cost(1, 50);
	    Money tax(0, 15), total;
	
	    // Binary "+" operator
	    total = cost + tax;
	    total.output(); // Displays $1.65
	
	    // Unary "-" operator
	    Money negativeCost = -cost;
	    negativeCost.output(); // Displays -$1.50
	
	    return 0;
	}
```
### Overloading Operators: Which Methods?
 Object-Oriented Programming (OOP) prensipleri, operatör aşırı yüklemelerinin sınıf üyesi olarak tanımlanmasını önerir. Bu, OOP'nin "ruhunu" korur ve genellikle daha verimli olur. İşte kısa bir açıklama:
#### Üye Operatörlerin Avantajları
1. **OOP'nin Ruhu**: Üye operatörler, sınıfın iç mantığını ve veri kapsüllemeyi korur, bu da OOP'nin temel prensiplerinden biridir.
2. **Verimlilik**: Üye operatörler, doğrudan sınıfın özel verilerine erişebilir, bu da accessor (erişim) ve mutator (değiştirici) fonksiyonları çağırma ihtiyacını ortadan kaldırır.
3. **Kodun Okunabilirliği**: Üye operatörler, sınıfın davranışlarını daha doğal ve anlaşılır kılar.
#### Üye Operatörlerin Dezavantajı
- **Simetri Sorunu**: Üye operatörler, operatörün her iki operandının da aynı sınıftan olması gerektiği durumlarda simetri sorunlarına yol açabilir. Örneğin, `Money` sınıfı için `Money + int` ve `int + Money` işlemlerini desteklemek zor olabilir. Bu durumda, bağımsız (standalone) operatör fonksiyonları daha esnek olabilir.
### Overloading Function Application ()
 Fonksiyon çağrı operatörü `()` yalnızca üye fonksiyon olarak aşırı yüklenebilir. Bu, bir sınıf nesnesinin bir fonksiyon gibi kullanılmasına olanak tanır.
#### Neden Kullanılır?
- **Fonksiyon Gibi Kullanım**: Sınıf nesnelerinin bir fonksiyon gibi çağrılmasını sağlar.
- **Esneklik**: Farklı sayıda ve türde argümanlarla aşırı yüklenebilir.
```cpp
	class Aclass {
	public:
	    // Overload function call operator
	    void operator()(int x) const {
	        std::cout << "Called with argument: " << x << std::endl;
	    }
	};
```
**Kullanım:**
```cpp
	int main() {
	    Aclass anObject;
	    anObject(42); // Calls the overloaded function call operator
	
	    return 0;
	}
```
### ### `&&`, `||` ve Virgül (,) Operatörlerinin Aşırı Yüklenmesi

- **Kısa Devre Değerlendirmesi**: `&&` ve `||` operatörleri, kısa devre değerlendirmesi kullanır (ilk operand sonucu belirlerse ikinci operand değerlendirilmez).
- **Aşırı Yükleme Durumunda**: Aşırı yüklendiğinde, bu operatörler tam değerlendirme kullanır (her iki operand da her zaman değerlendirilir).
- **Virgül Operatörü**: Normalde soldaki ifadeyi atar, sağdaki ifadeyi döndürür. Aşırı yüklendiğinde bu davranış değişebilir.
- **Genel Öneri**: Bu operatörleri aşırı yüklemek genellikle önerilmez çünkü beklenen davranışlarını kaybederler ve kodun anlaşılmasını zorlaştırabilir.
# Friends and Automatic Type Conversion
## Friend Functions, Friend Classes
C++'da sınıf üyesi olmayan fonksiyonlar, sınıfın bir parçası olmayan ancak o sınıfın nesneleri üzerinde işlem yapabilen fonksiyonlardır. Operatör aşırı yüklemeleri bu şekilde yapılabilir. Ancak, bu fonksiyonlar sınıfın özel verilerine erişmek için genellikle erişimci (getter) ve değiştirici (setter) fonksiyonlarını kullanır, bu da verimsizdir.

Bu verimsizliği önlemek için, bu operatör aşırı yüklemelerini sınıfın arkadaş (friend) fonksiyonları olarak tanımlayabilirsiniz. Arkadaş fonksiyonlar, sınıfın özel ve korumalı üyelerine doğrudan erişebilir, böylece ek fonksiyon çağrısı gereksinimini ortadan kaldırır ve daha verimli olur.

Örnek:
```cpp
#include <iostream>

class MyClass {
private:
    int value;

public:
    MyClass(int v) : value(v) {}

    // Arkadaş fonksiyon bildirimi
    friend MyClass operator+(const MyClass& lhs, const MyClass& rhs);

    void display() const {
        std::cout << value << std::endl;
    }
};

// Arkadaş fonksiyon tanımı
MyClass operator+(const MyClass& lhs, const MyClass& rhs) {
    return MyClass(lhs.value + rhs.value);
}

int main() {
    MyClass a(5), b(10);
    MyClass c = a + b;
    c.display(); // 15
    return 0;
}
```
Bu şekilde, operatör aşırı yüklemeleri daha verimli hale gelir.

Bazı programcılar, arkadaş (friend) fonksiyonların Nesne Yönelimli Programlama (OOP) prensiplerine aykırı olduğunu düşünür. OOP'nin "ruhu", tüm operatörlerin ve fonksiyonların üye fonksiyonlar olmasını gerektirir. Bu görüşe göre, arkadaş fonksiyonlar sınıfın kapsülleme ilkesini ihlal eder çünkü sınıfın özel üyelerine doğrudan erişim sağlarlar.

Ancak, arkadaş fonksiyonların bazı avantajları vardır:

1. **Verimlilik**: Arkadaş fonksiyonlar, erişimci (getter) ve değiştirici (setter) fonksiyonları çağırma ihtiyacını ortadan kaldırarak verimliliği artırır.
2. **Otomatik Tür Dönüşümü**: Arkadaş fonksiyonlar, operatör aşırı yüklemelerinde otomatik tür dönüşümüne izin verir. Bu, operatörlerin daha esnek ve kullanışlı olmasını sağlar.
3. **Kapsülleme**: Arkadaş fonksiyonlar, sınıf tanımında belirtildiği için hala kapsülleme sağlar. Bu, sınıfın iç yapısının dışarıdan gizli kalmasını sağlar.

Özetle, arkadaş fonksiyonlar bazı OOP prensiplerine aykırı gibi görünse de, özellikle operatör aşırı yüklemelerinde sağladıkları verimlilik ve esneklik nedeniyle avantajlıdırlar.

### Friend Classes
C++'da, bir sınıfın tüm üye fonksiyonlarını başka bir sınıfa arkadaş olarak tanımlayabilirsiniz. Bu, bir fonksiyonun bir sınıfa arkadaş olmasına benzer, ancak bu durumda tüm sınıfın üye fonksiyonları arkadaş olur. Örneğin, `class F` `class C`'nin arkadaşı olarak tanımlandığında, `class F`'nin tüm üye fonksiyonları `class C`'nin özel ve korumalı üyelerine erişebilir.

Önemli noktalar:

- Arkadaşlık karşılıklı değildir; yani `class F` `class C`'nin arkadaşı olduğunda, `class C` `class F`'nin özel üyelerine erişemez.
- Arkadaşlık verilir, alınmaz; yani bir sınıf başka bir sınıfa arkadaşlık vermez, sadece arkadaşlık tanımlar.
- Arkadaş sınıf tanımı, "yetkilendiren" sınıfın tanımının içine `friend class F` şeklinde yazılır.

Örnek:
```cpp
#include <iostream>

class F; // İleri bildirim

class C {
private:
    int value;

public:
    C(int v) : value(v) {}

    // F sınıfını arkadaş olarak tanımlama
    friend class F;
};

class F {
public:
    void showValue(const C& c) {
        std::cout << c.value << std::endl; // C sınıfının özel üyesine erişim
    }
};

int main() {
    C c(42);
    F f;
    f.showValue(c); // 42
    return 0;
}
```
Bu örnekte, `class F` `class C`'nin arkadaşı olarak tanımlanmıştır, bu nedenle `F`'nin üye fonksiyonları `C`'nin özel üyelerine erişebilir.

## Constructors for Automatic Type Conversion
# References and More Overloading
Referans, bir depolama konumunun adıdır ve bir "pointer" (işaretçi) ile benzerdir. Ancak, referanslar doğrudan bir değişkenin bellekteki konumuna işaret eder ve bu değişkenin başka bir adıdır. Referanslar tanımlandıktan sonra başka bir değişkeni işaret edemezler.

Örnek:
```cpp
int robert;
int& bob = robert; // bob, robert'in referansıdır
```
Bu durumda, `bob` değişkeni `robert` değişkeninin depolama konumuna referans olur. `bob` üzerinde yapılan değişiklikler doğrudan `robert` üzerinde de etkili olur.

Örnek kullanım:
```cpp
#include <iostream>

int main() {
    int robert = 10;
    int& bob = robert; // bob, robert'in referansıdır

    bob = 20; // bob'u değiştirmek robert'i de değiştirir

    std::cout << "robert: " << robert << std::endl; // 20
    std::cout << "bob: " << bob << std::endl; // 20

    return 0;
}
```
Bu örnekte, `bob` referansı `robert` değişkenine bağlanmıştır. `bob` üzerinde yapılan değişiklikler `robert` üzerinde de etkili olur. Bu nedenle, `bob`'u 20 olarak değiştirdiğimizde, `robert` de 20 olur.

Referanslar, doğrudan bir değişkenin bellekteki konumuna işaret ettiği için, yanlış kullanıldığında beklenmedik sonuçlara yol açabilir. Örneğin, bir referansın geçersiz bir değişkene işaret etmesi durumunda bellek hataları oluşabilir.

***Faydalı Kullanım Durumları***
1. **Call-by-Reference (Referans ile Çağırma)**:
    - Fonksiyonlara argüman olarak referanslar geçildiğinde, fonksiyon bu argümanların orijinal değişkenlerini değiştirebilir. Bu, büyük veri yapılarının kopyalanmasını önleyerek performansı artırır.
2. **Referans Döndürme**:
	- Fonksiyonlar, bir değişkenin referansını döndürebilir. Bu, operatör aşırı yüklemelerinin daha doğal bir şekilde yazılmasını sağlar.
3. **Alias (Takma Ad) Olarak Düşünme**
	- Referansları, bir değişkenin takma adı olarak düşünebilirsiniz. Bir referans, orijinal değişkenin başka bir adı gibi davranır ve bu nedenle referans üzerinden yapılan değişiklikler orijinal değişkeni etkiler.

Bu şekilde, referanslar hem performans avantajları sağlar hem de kodun daha okunabilir ve doğal olmasına yardımcı olur.

### Returning Reference
***Sözdizimi:*** `int& getElement(int arr[], int index);`
- `int&`: Fonksiyonun döndüreceği değerin türü ve bunun bir referans olduğunu belirtir.
- `int arr[]`: Fonksiyonun aldığı parametre, bir dizi.
- `int index`: Dizinin indeksini belirtir.

Örnek:
```cpp
int& getElement(int arr[], int index) {
    return arr[index]; // Dizinin bir elemanının referansını döndürür
} 

int main() {
    int myArray[5] = {1, 2, 3, 4, 5};
    getElement(myArray, 2) = 10; // myArray[2] = 10
    std::cout << myArray[2] << std::endl; // 10

    return 0;
}
```
Bu örnekte:
- `getElement` fonksiyonu, bir dizinin belirli bir indeksindeki elemanın referansını döndürür.
- `getElement(myArray, 2) = 10;` ifadesi, `myArray[2]` elemanını 10 yapar.
- `myArray[2]`'nin değeri 10 olarak güncellenir.

***Özetle:***
- Referans döndüren fonksiyonlar, bir değişkenin bellekteki konumunu döndürür.
- Bu sayede, fonksiyonun döndürdüğü referans üzerinden yapılan değişiklikler, orijinal değişkeni etkiler.
## << and >>
***Örnek:*** 
```cpp
#include <iostream>

class MyClass {
private:
    int value;

public:
    MyClass(int v = 0) : value(v) {}

    // Arkadaş fonksiyon olarak << operatörünü aşırı yükleme
    friend std::ostream& operator<<(std::ostream& os, const MyClass& obj) {
        os << obj.value;
        return os;
    }

    // Arkadaş fonksiyon olarak >> operatörünü aşırı yükleme
    friend std::istream& operator>>(std::istream& is, MyClass& obj) {
        is >> obj.value;
        return is;
    }
};

int main() {
    MyClass myObject(10);

    // Çıktı operatörü kullanımı
    std::cout << "MyObject: " << myObject << std::endl;

    // Girdi operatörü kullanımı
    std::cout << "Enter new value for MyObject: ";
    std::cin >> myObject;

    std::cout << "Updated MyObject: " << myObject << std::endl;

    return 0;
}
```

Bu örnekte:
- `<<` operatörü aşırı yüklenerek `MyClass` nesnesinin `std::cout` ile nasıl yazdırılacağı tanımlanmıştır.
- `>>` operatörü aşırı yüklenerek `MyClass` nesnesinin `std::cin` ile nasıl okunacağı tanımlanmıştır.
- Bu sayede, `myObject.output()` gibi özel fonksiyonlar yerine `std::cout << myObject` ve `std::cin >> myObject` kullanarak daha okunabilir ve doğal bir kod yazılabilir.
#### `<<` Operatörü (Insertion Operator)
- `<<` operatörü, `cout` ile birlikte kullanılarak verilerin ekrana yazdırılmasını sağlar.
- Bu operatör, iki operand alır: `cout` nesnesi ve yazdırılacak veri.
- Örneğin, `std::cout << "Hello";` ifadesi, `"Hello"` stringini ekrana yazdırır.

#### `>>` Operatörünün Aşırı Yüklenmesi
```cpp
#include <iostream>

class Money {
private:
    int amount;

public:
    Money(int a = 0) : amount(a) {}

    // Arkadaş fonksiyon olarak << operatörünü aşırı yükleme
    friend std::ostream& operator<<(std::ostream& os, const Money& m) {
        os << m.amount;
        return os;
    }

    // Arkadaş fonksiyon olarak >> operatörünü aşırı yükleme
    friend std::istream& operator>>(std::istream& is, Money& m) {
        is >> m.amount;
        return is;
    }
};

int main() {
    Money amount(100);

    // << operatörü kullanımı
    std::cout << "I have " << amount << std::endl;

    // >> operatörü kullanımı
    std::cout << "Enter new amount: ";
    std::cin >> amount;

    std::cout << "Updated amount: " << amount << std::endl;

    return 0;
}
```
Özetle
- `<<` operatörü aşırı yüklenerek `Money` nesnesinin `std::cout` ile nasıl yazdırılacağı tanımlanmıştır.
- `>>` operatörü aşırı yüklenerek `Money` nesnesinin `std::cin` ile nasıl okunacağı tanımlanmıştır.
- Bu sayede, `amount.output()` gibi özel fonksiyonlar yerine `std::cout << amount` ve `std::cin >> amount` kullanarak daha okunabilir ve doğal bir kod yazılabilir.

`<<` operatörü, zincirleme (cascade) işlemlerine izin vermek için `ostream` nesnesini geri döndürmelidir.
## Operators: =, [], ++, --
### Assignment Operator, =
- C++'da, atama operatörü (`=`) varsayılan olarak üye değişkenlerin birebir kopyalanmasını sağlar.
- Bu, basit sınıflar için genellikle yeterlidir.
- Eğer sınıfınız dinamik bellek yönetimi (pointer'lar) kullanıyorsa, varsayılan atama operatörü yeterli olmayabilir.
- Bu durumda, kendi atama operatörünüzü yazmanız gerekir.

```cpp
#include <iostream>

class MyClass {
private:
    int* data;

public:
    MyClass(int value) {
        data = new int(value);
    }

    // Kopya yapıcı
    MyClass(const MyClass& other) {
        data = new int(*other.data);
    }

    // Özel atama operatörü
    MyClass& operator=(const MyClass& other) {
        if (this == &other) {
            return *this; // Kendine atama kontrolü
        }
        delete data; // Eski veriyi serbest bırak
        data = new int(*other.data); // Yeni veriyi kopyala
        return *this;
    }

    ~MyClass() {
        delete data;
    }

    void display() const {
        std::cout << *data << std::endl;
    }
};

int main() {
    MyClass obj1(10);
    MyClass obj2(20);

    obj2 = obj1; // Atama operatörü kullanımı

    obj1.display(); // 10
    obj2.display(); // 10

    return 0;
}
```
Bu örnekte:
- `MyClass` sınıfı dinamik bellek yönetimi kullanır (pointer ile).
- Özel atama operatörü (`operator=`) yazılmıştır.
- Atama operatörü, kendine atama kontrolü yapar, eski veriyi serbest bırakır ve yeni veriyi kopyalar.
### `++` ve `--` Operatörlerinin Aşırı Yüklenmesi

#### Ön Ek (Prefix) Notasyonu
Ön ek notasyonu, operatörün değişkenin değerini artırmadan veya azaltmadan önce çalıştığı durumu ifade eder.
```cpp
class MyClass {
private:
    int value;

public:
    MyClass(int v = 0) : value(v) {}

    // Ön ek (prefix) ++ operatörünün aşırı yüklenmesi
    MyClass& operator++() {
        ++value;
        return *this;
    }

    void display() const {
        std::cout << value << std::endl;
    }
};
```

#### Son Ek (Postfix) Notasyonu
Son ek notasyonu, operatörün değişkenin değerini artırdıktan veya azalttıktan sonra çalıştığı durumu ifade eder. Bu notasyonu aşırı yüklemek için, fonksiyona `int` türünde bir parametre eklenir. Bu parametre sadece derleyiciye son ek notasyonunun kullanıldığını belirtmek için kullanılır.

```cpp
class MyClass {
private:
    int value;

public:
    MyClass(int v = 0) : value(v) {}

    // Ön ek (prefix) ++ operatörünün aşırı yüklenmesi
    MyClass& operator++() {
        ++value;
        return *this;
    }

    // Son ek (postfix) ++ operatörünün aşırı yüklenmesi
    MyClass operator++(int) {
        MyClass temp = *this;
        value++;
        return temp;
    }

    void display() const {
        std::cout << value << std::endl;
    }
};

int main() {
    MyClass obj(10);

    ++obj; // Ön ek kullanımı
    obj.display(); // 11

    obj++; // Son ek kullanımı
    obj.display(); // 12

    return 0;
}
```
Bu örnekte:
- `operator++()` fonksiyonu, ön ek (prefix) `++` operatörünü aşırı yükler.
- `operator++(int)` fonksiyonu, son ek (postfix) `++` operatörünü aşırı yükler. `int` parametresi sadece derleyiciye son ek notasyonunun kullanıldığını belirtmek için kullanılır.

### `[]` Operatörünün Aşırı Yüklenmesi
1. **Üye Fonksiyon Olmalı**: `[]` operatörü, sınıfın bir üye fonksiyonu olarak aşırı yüklenmelidir.
2. **Referans Döndürmeli**: `[]` operatörü, bir referans döndürmelidir. Bu, operatörün döndüğü değerin değiştirilebilmesini sağlar.
```cpp
#include <iostream>

class MyArray {
private:
    int* data;
    int size;

public:
    MyArray(int s) : size(s) {
        data = new int[size];
    }

    ~MyArray() {
        delete[] data;
    }

    // [] operatörünün aşırı yüklenmesi
    int& operator[](int index) {
        if (index >= 0 && index < size) {
            return data[index];
        } else {
            throw std::out_of_range("Index out of range");
        }
    }

    // [] operatörünün const versiyonu
    const int& operator[](int index) const {
        if (index >= 0 && index < size) {
            return data[index];
        } else {
            throw std::out_of_range("Index out of range");
        }
    }
};

int main() {
    MyArray arr(5);

    // Değer atama
    arr[0] = 10;
    arr[1] = 20;

    // Değer okuma
    std::cout << "arr[0]: " << arr[0] << std::endl; // 10
    std::cout << "arr[1]: " << arr[1] << std::endl; // 20

    return 0;
}
```
Bu örnekte:
- `MyArray` sınıfı, dinamik bir dizi yönetir.
- `operator[]` fonksiyonu, `[]` operatörünü aşırı yükler ve bir referans döndürür.
- Bu sayede, `arr[0] = 10;` gibi ifadelerle dizinin elemanlarına erişebilir ve onları değiştirebilirsiniz.