*Links*: [[00 - Index]]
*Date*: 16.10.2024
*Resources*: [name]()

---
# Constructors
- Yapıcı fonksiyonlar (Constructors), bir sınıfın yeni bir örneği oluşturulduğunda nesnenin **başlatılmasından** sorumludur.
- Nesnenin (object) üye değişkenlerini (members) başlatmak için kullanılır.
- Constructor'lar, üye değişkenlerin başlatılmasının yanı sıra, nesne oluşturulurken yapılması gereken diğer işlemleri de gerçekleştirebilir.
- Constructor'lar, sınıfın özel bir üyesidir ve sınıf adıyla aynı isme sahiptir.
- Constructor'lar, nesne oluşturulduğunda otomatik olarak çağırılır.
- Nesnelerin doğru ve tam olarak başlatılmasını sağladıkları için çok kullanışlıdırlar.
- Constructor'lar, Nesne Yönelimli Programlamanın (OOP) temel ilkelerinden biridir.
- Yapıcılar (constructors) yalnızca üye değişkenleri başlatmak için değil, aynı zamanda verileri doğrulamak ve uygun olmayan verilerin atanmasını engellemek için de kullanılabilir. Bu, Nesne Yönelimli Programlamanın (OOP) güçlü bir ilkesidir.
- Örnek bir Constructor:
	```cpp
		class MyClass {
		public:
		    int x;
		    MyClass(int val) {  // Constructor
		        x = val;
		    }
		};
		
		int main() {
		    MyClass obj(10);  // Constructor is called here
		    return 0;
		}
	```
#### Constructor'ların neden return değeri olmaz?
- **Dil Özellikleri**: C++, Java ve C# gibi dillerde, constructor'ların geri dönüş tipi belirtmemesi bir dil kuralıdır. Bu, dilin yapısı ve kuralları gereği böyledir.
- **Bellek Yönetimi**: Constructor'lar, nesnenin bellekteki yerini ayırır ve initialize eder. Bu işlem sırasında bir geri dönüş değeri verilmesi gereksizdir çünkü nesne zaten oluşturulmuş ve başlatılmıştır.
### Definitions
- Constructor'lar, diğer üye fonksiyonlar gibi tanımlanır, ancak bazı farklılıkları vardır.
- **Sınıf (Class) ile Aynı İsimde Olmalıdır**: Constructor'lar, sınıfın adıyla aynı isme sahip olmalıdır. Bu, derleyicinin bunları diğer üye fonksiyonlardan ayırt etmesini sağlar.
- Constructor'lar, sınıf tanımında belirtildiği gibi aynı şekilde tanımlanır, ancak sınıfın dışında tanımlandığında `::` operatörü kullanılır.
- **Değer Döndüremezler**: Yapıcılar, geri dönüş değeri belirtemezler; hatta `void` bile döndüremezler. Bu, dilin kuralıdır ve yapıcıların geri dönüş değeri belirtmemesi, nesne oluşturma sürecini basitleştirir ve daha tutarlı hale getirir.
- **Public Bölümünde Olmalıdır**: Constructor'lar genellikle sınıfın public (genel) bölümünde tanımlanır. Eğer private (özel) bölümde tanımlanmış olsaydı, dışarıdan nesneler oluşturulamazdı. Bu, nesnelerin sınıf dışından erişilebilir ve kullanılabilir olmasını sağlar.
- **Nesne Oluşturulduğunda Çağrılır**: Yapıcılar, bir nesne oluşturulduğunda otomatik olarak çağrılır. Bu, nesnenin başlatılması ve gerekli başlangıç işlemlerinin yapılmasını sağlar.
#### Initialization List Kullanımı
- Initialization List, yapıcı fonksiyonun başında `:` işareti ile başlar ve üye değişkenlerin yanına atanacak değerler parantez içinde yazılır. Bu, üye değişkenlerin doğrudan başlatılmasını sağlar ve performans açısından daha verimlidir. Örnek olarak:
	```cpp
		DayOfYear::DayOfYear(int monthValue, int dayValue)
		    : month(monthValue), day(dayValue)
		{
		    // Body left empty
		}
	```
	Bu örnekte, yapıcı fonksiyon `month` ve `day` üye değişkenlerini başlatmak için "Initialization List" kullanır. Bu, üye değişkenlerin doğrudan başlatılmasını sağlar.
- Sabit (`const`) veya referans (`reference`) üye değişkenler sadece Initialization List ile başlatılabilir.
### Calling
- **Argümanların Constructor'a Geçirilmesi**:  Parantez içindeki değerler, yapıcı fonksiyona argüman olarak geçirilir. Örneğin: `date1(7, 4)` çağrıldığında, `7` ve `4` değerleri yapıcıya argüman olarak geçer.
- Constructor'lar, diğer üye fonksiyonlar gibi çağrılamaz. Örnek olarak:
	```cpp
		DayOfYear date1, date2  
		date1.DayOfYear(7, 4); // ILLEGAL!  
		date2.DayOfYear(5, 5); // ILLEGAL!
	```
	
  Constructor'lar, nesne oluşturulma ve başlatılma aşamasında otomatik olarak çağrılırlar. Bir nesne zaten oluşturulduktan sonra, constructor'ı tekrar çağırmak mantıksal olarak anlamsızdır ve dilin kuralları gereği izin verilmez. Bu yüzden, constructor'lar normal üye fonksiyonlar gibi çağrılamaz.
#### Overloaded Constructors
Yapıcılar (constructors) da diğer fonksiyonlar gibi aşırı yüklenebilir (overload) ve farklı parametre listelerine sahip olabilir.
- **Fonksiyon İmzası**:  
    Bir fonksiyonun imzası, fonksiyonun adını ve parametre listesini içerir. Aynı isimde ancak farklı parametre listelerine sahip fonksiyonlar tanımlanabilir.
- **Yapıcıların Aşırı Yüklenmesi**:  
    Bir sınıfta birden fazla yapıcı tanımlanabilir ve her biri farklı sayıda veya türde parametre alabilir. Bu, farklı durumlar için nesnelerin farklı şekillerde oluşturulmasını sağlar.
- Örnek:
	```cpp
		class DayOfYear {
		public:
		    // No-parameter constructor
		    DayOfYear() : month(1), day(1) {}
		
		    // Constructor with one parameter
		    DayOfYear(int monthValue) : month(monthValue), day(1) {}
		
		    // Constructor with two parameters
		    DayOfYear(int monthValue, int dayValue) : month(monthValue), day(dayValue) {}
		
		private:
		    int month;
		    int day;
		};
	```
#### Default Contructor vs No-parameter Constructor
- **No-Parameter Constructor**: Parametre almaz ve doğrudan nesne oluşturur.
- **Default Constructor**: Parametre almaz ve bir sınıfın herhangi bir yapıcı tanımlanmamışsa derleyici tarafından otomatik olarak sağlanır.
#### Argüman Almayan Contructor'lar
- **Nesne Bildirimleri**:
    ```cpp
	    DayOfYear date1;  // Correct way to declare an object with the default constructor
    ```
    Bu, `DayOfYear` sınıfından `date1` adlı bir nesne oluşturur. Parantez kullanılmaz.
- **Fonksiyon Deklarasyonu Karışıklığı**:
    ```cpp
	    DayOfYear date();  // This is actually a function declaration!
    ```
    Bu satır, `date` adında ve `DayOfYear` türünde bir nesne oluşturmak yerine, `DayOfYear` döndüren ve parametre almayan bir fonksiyonun prototipini bildirir. Bu, C++'ta yaygın bir hatadır ve dikkat edilmesi gerekir.
#### Bir Nesneyi Tekrar Oluşturma
- **Nesne Tanımlama ve Yapıcı Çağrısı**:
    ```cpp
	    DayOfYear holiday(7, 4);  
    ```  
    Bu satırda, `DayOfYear` sınıfından `holiday` adlı bir nesne oluşturulmuştur ve yapıcı fonksiyon çağrılarak `holiday` nesnesinin `month` ve `day` üye değişkenleri sırasıyla 7 ve 4 olarak başlatılmıştır.
- **Nesneyi Yeniden Başlatma (Re-initialize)**:
    ```cpp
	    holiday = DayOfYear(5, 5);
    ```
    Bu satırda, `DayOfYear` yapıcısı tekrar çağrılarak yeni bir "anonim nesne" oluşturulur. Bu anonim nesnenin `month` değeri 5 ve `day` değeri 5 olacak şekilde başlatılır. Bu anonim nesne daha sonra mevcut `holiday` nesnesine atanır.
- **Anonim Nesne (Anonymous Object)**:  
    `DayOfYear(5, 5)` ifadesi, yapıcı fonksiyonun çağrılmasıyla oluşturulan ve geçici olarak var olan bir anonim nesnedir. Bu anonim nesne, oluşturulduktan sonra `holiday` nesnesine atanır.
- **Atama İşlemi**:  
    Atama işlemi, mevcut `holiday` nesnesinin üye değişkenlerinin yeni anonim nesnenin üye değişkenleriyle değiştirilmesini sağlar. Böylece, `holiday` nesnesi yeniden başlatılmış olur.

Bu yöntem, bir nesneyi yeniden başlatmak için kullanışlıdır ve mevcut nesneyi yeni bir anonim nesne ile değiştirerek üye değişkenlerini günceller.

#### Default Constructor
- **Varsayılan Yapıcı (Default Constructor)**: Parametresiz bir constructor'dır. Eğer sınıfta herhangi bir constructor tanımlanmadıysa, derleyici otomatik olarak bir varsayılan yapıcı (default constructor) oluşturur.
- **Otomatik Oluşturma Durumu**:
    - Eğer sınıfta **hiçbir constructor tanımlanmadıysa**, derleyici otomatik olarak bir default constructor oluşturur.
    - Eğer sınıfta **herhangi bir constructor tanımlandıysa** (parametreli veya parametresiz), derleyici otomatik olarak bir varsayılan constructor oluşturmaz.

#### Class Tipindeki Üye Değişkenler (Class içinde Class)
Nesne Yönelimli Programlamada (OOP), bir sınıfın üye değişkenlerinin başka sınıfların nesneleri olabilmesi, güçlü bir OOP ilkesidir. Bu tür ilişkilere genellikle "has-a" ilişkisi (composition) denir. 
- **"Has-a" İlişkisi (Composition)**:  
    Bir sınıfın üye değişkeni olarak başka bir sınıfın nesnesi bulunabilir. Bu, bir sınıfın diğer sınıfların işlevselliğinden yararlanmasını sağlar.
    ```cpp
    class Engine {
    public:
        Engine(int power) : power(power) {}
    private:
        int power;
    };
    
    class Car {
    public:
        Car(int enginePower) : engine(enginePower) {}
    private:
        Engine engine;  // Car "has-a" Engine
    };
    ```
- **Initialization List Kullanımı**:  
    Üye değişkeni olarak başka bir sınıfın nesnesi bulunduğunda, bu nesnenin yapıcısını çağırmak için Initialization List kullanılır. Bu, üye değişkenlerin doğru ve verimli bir şekilde başlatılmasını sağlar.
- Constructor'ların Çağrılması**:  
    Bir sınıfın yapıcısı, üye değişkeni olan diğer sınıfın yapıcısını Initialization List kullanarak çağırır.
    ```cpp
    Car::Car(int enginePower) : engine(enginePower) {
        // Additional initialization if needed
    }
    ```
- **OOP'nin Gücü**:  
    Bu yaklaşım, sınıflar arasında güçlü bir ilişki kurar ve kodun yeniden kullanılabilirliğini artırır. Bir sınıf, başka bir sınıfın özelliklerini ve işlevlerini kendi içinde kullanarak daha karmaşık davranışlar oluşturabilir.
    
Özetle, bir sınıfın üye değişkeni olarak başka sınıfların nesnelerini kullanmak, OOP'nin güçlü bir prensibidir ve Initialization List kullanarak yapıcıların doğru şekilde çağrılması bu ilişkilerin doğru kurulmasını sağlar.
#### Parameter Passing Methods
1. **Call-by-Value (Değer ile Çağırma)**:
	- Argüman olarak geçirilen değerin bir kopyası yapılır.
	- Bu kopyalama işlemi ek yük oluşturur, özellikle büyük veri yapıları veya sınıf türleri için.
	- Basit türler (int, char, vb.) için bu ek yük ihmal edilebilir düzeydedir.
2. **Call-by-Reference (Referans ile Çağırma)**:    
	- Argüman olarak geçirilen değerin kendisi yerine bir referansı (adres) kullanılır.
	- Asıl argümanın bir yer tutucusu olarak işlev görür.
	- Kopyalama işlemi gerekmediğinden, büyük veri yapıları veya sınıf türleri için çok daha verimlidir.
	- Özellikle büyük veri yapıları ve sınıf türleri için çağrı maliyetini düşürür.

Sonuç olarak, büyük veri yapıları ve sınıf türleri için call-by-reference yöntemi tercih edilir, çünkü kopyalama işlemi gerektirmez ve daha verimli çalışır. Bu yöntem, bellekte gereksiz kopyalamaları önleyerek performansı artırır.
# More Tools
### const parameter modifier
### Inline Functions
### Static member data
# Vectors
