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
## Constructors for Automatic Type Conversion
# References and More Overloading
## << and >>
## Operators: =, [], ++, --