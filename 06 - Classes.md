*Links*: [[00 - Index]]
*Date*: 15.10.2024
*Resources*: [Absolute C++ 6th Edition]()

---
# Structures
- Farklı türdeki verileri bir araya getirerek tek bir birim olarak işlem yapmayı sağlar.
- **Aggregate Data Type (Toplu Veri Türü)**: Birden fazla veriyi bir araya getirerek tek bir birim olarak işlem yapmayı sağlar. Diziler ve struct'lar bu tür veri yapılarıdır.
### Structure Types
- Struct tanımlamaları genelde global olarak yapılır. Bu, struct'ın tüm programda kullanılabilir olmasını sağlar.
- Struct tanımlaması, bellekte herhangi bir yer ayırmaz. Sadece struct'ın nasıl görüneceğini belirten bir şablon sağlar.
- Struct'lar, farklı türdeki verileri bir araya getirerek daha karmaşık veri yapıları oluşturmanıza olanak tanır ve kodunuzu daha düzenli ve okunabilir hale getirir.
- [[06.01 - Struct Definition|Struct Definition]]
- Struct'ların içindeki değişkenlere member variables (üye değişkenler) denir.
- Farklı struct'lar aynı isimde üye değişkenlere sahip olabilirler. Bu, herhangi bir çakışmaya neden olmaz çünkü her struct, kendi üye değişkenlerini bağımsız olarak tanımlar ve kullanır.
- Struct tanımlamalarının sonunda mutlaka `;` olmalıdır. Çünkü `;`'den önce değişken tanımlamaları yapılabilir.
- Struct türünde iki değişken arasında yapılan atama işlemi, bir struct'ın tüm üye değişkenlerinin değerlerini diğer struct'ın üye değişkenlerine kopyalar. Örnek:
	```cpp
		#include <iostream>
		#include <string>
		
		// Global struct tanımlaması
		struct CropYield {
		    double weight;
		    int quantity;
		    std::string cropType;
		};
		
		int main() {
		    // CropYield türünde iki değişken tanımlama
		    CropYield apples, oranges;
		
		    // oranges değişkeninin üye değişkenlerine değer atama
		    oranges.weight = 150.5;
		    oranges.quantity = 200;
		    oranges.cropType = "Oranges";
		
		    // apples değişkenine oranges değişkeninin değerlerini kopyalama
		    apples = oranges;
		
		    // apples değişkeninin üye değişkenlerini ekrana yazdırma
		    std::cout << "Apples Weight: " << apples.weight << std::endl;
		    std::cout << "Apples Quantity: " << apples.quantity << std::endl;
		    std::cout << "Apples Crop Type: " << apples.cropType << std::endl;
		
		    return 0;
		}
	```
### Structures as Function Arguments
- Struct'lar (yapılar) C++ dilinde herhangi bir basit veri türü gibi fonksiyonlara parametre olarak geçirilebilir ve fonksiyonlardan geri döndürülebilir. Struct'lar, pass-by-value (değer ile geçirme), pass-by-reference (referans ile geçirme) veya bu yöntemlerin kombinasyonu ile fonksiyonlara geçirilebilir. Ayrıca, struct'lar fonksiyonlardan geri döndürülebilir (`Point createPoint(int x, int y) {} // Struct döndüren fonksiyon`).
### Initializing Structures
# Classes
Sınıflar, int ve double gibi tam teşekküllü veri türleridir; bu türden değişkenler "nesne" olarak adlandırılır, fonksiyonlara parametre olarak geçebilir (değer veya referans ile) ve diğer veri türleri gibi kullanılabilir.

- Değerleri nesne (object) olarak adlandırılan bir türdür.
- Nesnelerin hem data'sı hem de member function'ları vardır.
- Member function'ların nesnelerinin data'sına özel olarak erişimi vardır.
- Struct'lara benzer şekilde, C++ dilinde sınıflar (classes) da veri üyeleri (member data) ve üye fonksiyonlar (member functions) içerebilir. Sınıflar, nesne yönelimli programlamanın (OOP) temel yapı taşlarıdır ve veri ile bu veriler üzerinde gerçekleştirilen işlemleri bir araya getirirler. 
- Sınıf türünde değişkenler, nesne (object) olarak adlandırılır.
- Sınıflar, veri üyeleri ve üye fonksiyonları bir araya getirerek daha karmaşık veri yapıları ve işlevsellik sağlar. Sınıflar, nesne yönelimli programlamanın temelini oluşturur ve veri ile bu veriler üzerinde gerçekleştirilen işlemleri kapsüller.
- **Sınıflar (Classes)**: Veri üyeleri ve üye fonksiyonları bir araya getirerek daha karmaşık veri yapıları ve işlevsellik sağlar.
- **Nesneler (Objects)**: Sınıf türünde değişkenlerdir ve veri ile bu veriler üzerinde gerçekleştirilen işlemleri kapsüller.
- **Üye Fonksiyonlar**: Sınıf içinde tanımlanan ve sınıfın veri üyeleri üzerinde işlem yapan fonksiyonlardır.
### Defining Classes and Member Functions
- Sınıflar (classes) ve yapılar (structs) C++ dilinde benzer şekilde tanımlanır, ancak sınıflar, üye fonksiyonlar (member functions) içerebilir ve nesne yönelimli programlamanın temelini oluşturur. Sınıf tanımlarken, üye fonksiyonların sadece prototiplerini sınıf tanımı içinde belirtebilir ve bu fonksiyonların implementasyonlarını (gerçekleştirmelerini) sınıf tanımının dışında yapabilirsiniz.
- **Sınıf Tanımlama:** Bir sınıf tanımlarken, sınıfın adını, veri üyelerini ve üye fonksiyonların prototiplerini belirtirsiniz. Üye fonksiyonların gerçekleştirmeleri sınıf tanımının dışında yapılabilir.
- [[06.02 - Class Definition|Class Definition]]
- **Member Function:** Sınıf üye fonksiyonlarının implementasyonu, sınıf tanımının dışında `::` (scope resolution operator) kullanılarak yapılır ve bu operatör, fonksiyonun hangi sınıfa ait olduğunu belirtir.
- Nokta operatörü (`.`), belirli bir nesnenin üyesine erişmek için kullanılırken, scope resolution operatörü (`::`), bir fonksiyon tanımının hangi sınıfa ait olduğunu belirtir.
### Encapsulation
- Kapsülleme (encapsulation) nesne yönelimli programlamanın temel kavramlarından biridir. Kapsülleme, veriyi ve bu veri üzerinde gerçekleştirilebilecek işlemleri bir araya getirerek, veri ve işlevselliği bir sınıf içinde saklamayı ifade eder. Bu, veri gizliliğini ve bütünlüğünü korur ve kodun modülerliğini artırır.
- [[06.03 - Encapsulation|Encapsulation]]
- [[06.04 - Abstract Data Types|Abstract Data Types]]
- **OOP Prensipleri:** 
	1 - Bilgi  Gizliliği: İşlemlerin nasıl yapıldığının bilgisinin kullanıcı için gizlenmesi.
	2 - Data Abstraction: ADT/sınıf içinde verilerin nasıl işlendiğine dair ayrıntıların kullanıcı için gizlenmesi.
	3 - Encapsulation: Verileri ve işlemleri bir araya getirmek, ancak "ayrıntıları" gizli tutmak. 
### Public and Private Members
- C++ dilinde sınıflar (classes) kullanılarak kapsülleme (encapsulation) sağlanırken, veri üyeleri genellikle `private` olarak tanımlanır. Bu, nesne yönelimli programlamanın (OOP) temel ilkelerini destekler ve veri gizliliğini sağlar.
- Genelde önce public olan üyeleri tanımlayın.
#### Veri Üyelerinin `private` Olarak Tanımlanması:
- **Veri Gizliliği**: Veri üyeleri `private` olarak tanımlandığında, bu verilere doğrudan dışarıdan erişim engellenir. Bu, verinin yanlışlıkla değiştirilmesini veya bozulmasını önler.
- **Kapsülleme**: Veri ve bu veri üzerinde gerçekleştirilebilecek işlemleri bir araya getirir ve veri gizliliğini sağlar.
- **Üye Fonksiyonlar**: Veri üyelerine erişim ve bu veriler üzerinde işlem yapma, sadece `public` olarak tanımlanan üye fonksiyonlar aracılığıyla gerçekleştirilir.
#### Üye Fonksiyonların `public` Olarak Tanımlanması:
- **Kullanıcı Erişimi**: `public` olarak tanımlanan üye fonksiyonlar, sınıfın dışından erişilebilir ve kullanılabilir. Bu fonksiyonlar, veri üyeleri üzerinde işlem yapma yetkisine sahiptir.
- **Veri Manipülasyonu**: Kullanıcılar, veri üyeleri üzerinde sadece belirli üye fonksiyonlar aracılığıyla işlem yapabilirler. Bu, veri bütünlüğünü korur ve güvenliği artırır.
Örnek:
```cpp
	#include <iostream>
	#include <string>
	
	class Person {
	public:
	    // Kurucu fonksiyon (constructor)
	    Person(std::string personName, int personAge) {
	        name = personName;
	        age = personAge;
	    }
	
	    // Üye fonksiyonlar (operations on the data)
	    void displayInfo() {
	        std::cout << "Name: " << name << ", Age: " << age << std::endl;
	    }
	
	    void setName(std::string newName) {
	        name = newName;
	    }
	
	    void setAge(int newAge) {
	        age = newAge;
	    }

	private:
	    // Veri üyeleri (data values)
	    std::string name;
	    int age;
	};
	
	int main() {
	    // Person sınıfı türünde bir nesne oluşturma
	    Person person("Alice", 30);
	
	    // Üye fonksiyonları kullanma
	    person.displayInfo(); // Name: Alice, Age: 30
	
	    person.setName("Bob");
	    person.setAge(25);
	    person.displayInfo(); // Name: Bob, Age: 25
	
	    return 0;
	}
```
### Accessor and Mutator Functions
Tabii, C++ dilinde sınıflar kullanılarak veri üyelerine erişim ve bu veriler üzerinde işlem yapma, accessor (erişim) ve mutator (değiştirici) üye fonksiyonlar aracılığıyla gerçekleştirilir.
#### Accessor (Erişim) Üye Fonksiyonlar:
- **Amaç**: Veri üyelerini okumak için kullanılır.
- **Diğer Adı**: "Get" üye fonksiyonlar olarak da adlandırılır.
- **Özellik**: Veri üyelerini değiştirmez, sadece değerlerini döndürür.
#### Mutator (Değiştirici) Üye Fonksiyonlar:
- **Amaç**: Veri üyelerini değiştirmek için kullanılır.
- **Özellik**: Veri üyelerini uygulamanın gereksinimlerine göre manipüle eder.
##### Örnek:
Aşağıda, accessor ve mutator üye fonksiyonları içeren bir `Person` sınıfı örneği bulunmaktadır:

```cpp
#include <iostream>
#include <string>

class Person {
private:
    // Veri üyeleri
    std::string name;
    int age;

public:
    // Kurucu fonksiyon
    Person(std::string personName, int personAge) {
        name = personName;
        age = personAge;
    }

    // Accessor (erişim) üye fonksiyonlar
    std::string getName() const {
        return name;
    }

    int getAge() const {
        return age;
    }

    // Mutator (değiştirici) üye fonksiyonlar
    void setName(std::string newName) {
        name = newName;
    }

    void setAge(int newAge) {
        age = newAge;
    }
};

int main() {
    // Person sınıfı türünde bir nesne oluşturma
    Person person("Alice", 30);

    // Accessor üye fonksiyonları kullanma
    std::cout << "Name: " << person.getName() << std::endl; // Name: Alice
    std::cout << "Age: " << person.getAge() << std::endl;   // Age: 30

    // Mutator üye fonksiyonları kullanma
    person.setName("Bob");
    person.setAge(25);

    // Güncellenmiş değerleri okuma
    std::cout << "Updated Name: " << person.getName() << std::endl; // Updated Name: Bob
    std::cout << "Updated Age: " << person.getAge() << std::endl;   // Updated Age: 25

    return 0;
}
```

##### Özet:
- **Accessor Üye Fonksiyonlar**: Veri üyelerini okumak için kullanılır, veri üyelerini değiştirmez. Örneğin, `getName` ve `getAge`.
- **Mutator Üye Fonksiyonlar**: Veri üyelerini değiştirmek için kullanılır, uygulamanın gereksinimlerine göre veri üyelerini manipüle eder. Örneğin, `setName` ve `setAge`.

Accessor ve mutator üye fonksiyonlar, veri gizliliğini korurken veri üyelerine erişim ve bu veriler üzerinde işlem yapma olanağı sağlar. Bu, kapsülleme ilkesini destekler ve kodun güvenliğini artırır.

### Seperate Interface and Implementation
- Kapsülleme ilkesi gereği, sınıfın kullanıcıları sınıfın nasıl uygulandığını görmezler; sadece sınıfın "arayüzü" olan public üye fonksiyonları ve ilgili yorumları kullanarak sınıfla etkileşime girerler, sınıfın implementasyonu ise gizlidir. (Arayüz header dosyasında implementation cpp dosyasında)
### Structures vs Classes
- Struct'lar genellikle tüm üyeleri public olan ve üye fonksiyonları içermeyen veri yapılarıdır. 
- Sınıflar ise genellikle veri üyeleri private olan ve arayüz üye fonksiyonları public olan daha karmaşık veri yapılarıdır. 
- Teknik olarak struct ve class aynı mekanizmayı kullanır, ancak kullanım ve algı açısından farklılık gösterirler.
### Thinking Objects
OOP'de odak, algoritmalardan veriye kayar; algoritmalar hala var olup veriye odaklanır ve veriye uygun hale getirilir, yazılım tasarımında ise çeşitli nesneler ve bunların etkileşimleri tanımlanır.