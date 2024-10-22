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
- **Constructor'ların Çağrılması**:  
    Bir sınıfın yapıcısı, üye değişkeni olan diğer sınıfın yapıcısını Initialization List kullanarak çağırır.
    ```cpp
    Car::Car(int enginePower) : engine(enginePower) {
        // Additional initialization if needed
    }
    ```
- **OOP'nin Gücü**:  
    Bu yaklaşım, sınıflar arasında güçlü bir ilişki kurar ve kodun yeniden kullanılabilirliğini artırır. Bir sınıf, başka bir sınıfın özelliklerini ve işlevlerini kendi içinde kullanarak daha karmaşık davranışlar oluşturabilir.
    
Özetle, bir sınıfın üye değişkeni olarak başka sınıfların nesnelerini kullanmak, OOP'nin güçlü bir prensibidir ve Initialization List kullanarak yapıcıların doğru şekilde çağrılması bu ilişkilerin doğru kurulmasını sağlar.

####  Bir nesnenin yok olması: [[07.01 - Destructor]]
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
- Büyük veri tipleri (genellikle sınıflar) ile çalışırken, işlev çağrılarında referansla geçiş kullanmak genellikle tercih edilir. Bu, işlevin argümanı değiştirmeyecek olsa bile yapılır. Bunun nedeni, referansla geçiş yapmanın tüm nesneyi kopyalamak zorunda kalmaması ve bu sayede performans açısından maliyetli olabilecek kopyalama işlemlerinden kaçınılmasıdır.
- Argümanı korumak ve değiştirilmemesini sağlamak için sabit (const) parametre kullanılabilir.
- Eğer bir işlevin parametrelerini değiştirme gereksinimi yoksa, bu parametreleri `const` ile korumak iyi bir pratiktir.
- Bir fonksiyonun sonuna eklenen `const` anahtar kelimesi, bu fonksiyonun sınıfın üye verilerini değiştiremeyeceğini belirtir. Bu tür fonksiyonlara "const üye fonksiyonları" denir. Bu, fonksiyonun sınıfın durumu üzerinde hiçbir değişiklik yapmayacağını garanti eder. Örnek:

	```cpp
		class MyClass {
		public:
		    void displayData() const {
		        // Bu fonksiyon sınıfın üye verilerini değiştiremez
		        std::cout << memberData << std::endl;
		    }
		private:
		    int memberData;
		};
	```
- Bu örnekte, `displayData` fonksiyonu `const` olarak tanımlanmıştır, bu da `displayData` fonksiyonunun sınıfın `memberData` gibi üye verilerini değiştiremeyeceği anlamına gelir.
	```cpp
		class MyClass {
		public:
		    void ConstTest() const {
		        // Bu fonksiyon, sınıfın veri elemanlarını değiştiremez.
		        // const MyClass *p; gibi bir pointer ile çağrıldığında çalışır.
		        // const MyClass obj; gibi bir nesne ile çağrıldığında çalışır.
		        // Bu fonksiyon, sınıfın veri elemanlarını okuyabilir.
		
		        // num++;   // Hata: num, const fonksiyon içinde değiştirilemez.
		        count++; // Bu satırda hata yok. count, static olduğu için sınıfın tüm nesneleri tarafından paylaşılır.
		    }
		
		private:
		    static int count;
		    int num;
		};
	```
### Inline Functions
C++ dilinde `inline` fonksiyon, derleyiciye bu fonksiyonun çağrıldığı yerde fonksiyonun kodunu yerleştirmesi (inlining) talimatını veren bir fonksiyon türüdür. Bu, fonksiyon çağrısı sırasında oluşabilecek ek yükü ortadan kaldırarak performansı artırabilir. İşte detaylar:

- **Fonksiyonun Bildiriminde ve Tanımında `inline` Kullanımı:** `inline` anahtar kelimesi, fonksiyonun hem bildiriminde hem de tanımlanmasında kullanılabilir.
    ```cpp
    inline int add(int a, int b) {
        return a + b;
    }
    ```
    
- **Sınıf Üye Fonksiyonları:** Sınıf tanımı içinde yazılan fonksiyonlar otomatik olarak `inline` kabul edilir.
    ```cpp
    class MyClass {
    public:
        int multiply(int a, int b) const {
            return a * b;
        }
    };
    ```
    
- **Kısa Fonksiyonlar İçin İdeal:** `inline` fonksiyonlar en çok çok kısa fonksiyonlar için etkilidir. Uzun fonksiyonların inline yapılması, kod boyutunu artırabilir ve performans avantajını azaltabilir.
    
- **Çağrı Noktasına Kodun Yerleştirilmesi:** `inline` fonksiyonun kodu, fonksiyon çağrısının yapıldığı her yere yerleştirilir. Bu, işlev çağrısı sırasında oluşan ek yükü ortadan kaldırır.
    ```cpp
    inline void printMessage() {
        std::cout << "Hello, World!" << std::endl;
    }
    ```

Bu şekilde, `inline` fonksiyonlar küçük ve sık kullanılan fonksiyonlar için performans avantajı sağlar.
### Static member data
#### Static Members
C++ dilinde, `static` üye değişkenler, sınıfın tüm nesneleri tarafından "paylaşılan" tek bir kopyaya sahiptir. Bu, bir nesne bu değişkeni değiştirdiğinde, diğer tüm nesnelerin bu değişikliği görmesini sağlar. Bu tür değişkenler, belirli durumların takibi için kullanışlıdır, örneğin:

- Bir üye fonksiyonun kaç kez çağrıldığını izlemek.
- Belirli bir zamanda kaç tane nesnenin mevcut olduğunu saymak.
`static` üye değişkenler, türden önce `static` anahtar kelimesi ile tanımlanır.
Örnek:
```cpp
class MyClass {
public:
    MyClass() {
        ++objectCount; // Her nesne oluşturulduğunda sayacı artır
    }

    ~MyClass() {
        --objectCount; // Her nesne yok edildiğinde sayacı azalt
    }

    static int getObjectCount() {
        return objectCount; // Mevcut nesne sayısını döndür
    }

private:
    static int objectCount; // Tüm nesneler tarafından paylaşılan sayaç
};

// Sınıf dışındaki static üye değişkenin tanımı
int MyClass::objectCount = 0;
```

Bu örnekte:
- `MyClass` sınıfının `objectCount` adlı bir `static` üye değişkeni vardır.
- Bu sayaç, sınıfın tüm nesneleri tarafından paylaşılır ve nesne oluşturulup yok edildiğinde güncellenir.
- `getObjectCount` adlı `static` üye fonksiyonu, mevcut nesne sayısını döndürür.

Bu şekilde, `static` üye değişkenler, belirli durumların izlenmesini ve yönetilmesini sağlar.

#### Static Functions
C++ dilinde, üye fonksiyonlar `static` olarak tanımlanabilir. Bir üye fonksiyon, sınıfın üye verilerine erişim gerektirmiyorsa ve yine de sınıfın üyesi olması gerekiyorsa, bu fonksiyon `static` yapılabilir. `static` üye fonksiyonlar, sınıfın herhangi bir nesnesine bağlı değildir ve doğrudan sınıf adıyla çağrılabilir. İşte `static` üye fonksiyonların detayları:

- **Sınıfın Üye Verilerine Erişim Gerektirmez:**  
    `static` üye fonksiyonlar, sınıfın üye verilerine (non-static member variables) erişemez. Bu fonksiyonlar sadece `static` veriler ve `static` fonksiyonlar kullanabilir.
    
- **Sınıfın Bir Üyesi Olması Gerekir:**  
    Bu fonksiyonların hala sınıfın bir üyesi olması gerekiyorsa, `static` olarak tanımlanabilir.
    
- **Sınıf Dışından Çağrılabilir:**  
    `static` üye fonksiyonlar, sınıfın nesnesi olmadan doğrudan sınıf adıyla çağrılabilir. Örneğin, `Server::getTurn();`.
    
- **Sınıf Nesneleri Üzerinden de Çağrılabilir:**  
    `static` üye fonksiyonlar, sınıf nesneleri üzerinden de çağrılabilir. Örneğin, `myObject.getTurn();`.
    
- **Sadece `static` Veriler ve Fonksiyonlar Kullanabilir:**  
    `static` üye fonksiyonlar, sadece diğer `static` üyelerle etkileşimde bulunabilir.
    
Örnek:
```cpp
class Server {
public:
    static int getTurn() {
        return turn;
    }

    static void setTurn(int t) {
        turn = t;
    }
    
private:
    static int turn;
};

// Sınıf dışındaki static üye değişkenin tanımı
int Server::turn = 0;
```

Bu örnekte:
- `getTurn` ve `setTurn` fonksiyonları `static` olarak tanımlanmıştır.
- Bu fonksiyonlar doğrudan `Server` sınıfı adıyla çağrılabilir (`Server::getTurn();`).
- Ayrıca, bir sınıf nesnesi üzerinden de çağrılabilir (`myObject.getTurn();`), ancak bu durumda da `static` olarak kalırlar.
# Vectors
C++ dilinde, vektörler dinamik boyutlandırılabilen dizilerdir ve Standart Şablon Kütüphanesi (STL) kullanılarak şablon sınıfı (template class) olarak tanımlanır. Vektörler, program yürütülürken büyüyüp küçülebilirler.
### Vektörlerin Temel Özellikleri
- **Dinamik Boyutlandırma:** Vektörler, eleman ekleyip çıkartarak boyutlarını dinamik olarak değiştirebilirler.
- **Şablon Sınıfı (Template Class):** Vektörler, farklı veri türleri için kullanılabilir. `vector<Base_Type>` syntax'ı kullanılarak herhangi bir veri türü `Base_Type` olarak belirtilebilir.
- **Temel Veri Türü:** Vektörler, belirli bir temel türün (base type) değerlerinin koleksiyonunu saklar.
### Vektörler ve Diziler Arasındaki Benzerlikler
- **Temel Veri Türü:** Vektörler, diziler gibi belirli bir temel veri türü ile tanımlanır ve bu türün değerlerini saklar.
- **Dizi Gibi Erişim:** Vektörler, diziler gibi indekslenerek elemanlarına erişilebilir.
### Vektörlerin Deklarasyonu
- **Syntax:**
    ```cpp
    std::vector<int> v;
    ```
    
    Bu, `int` türünde bir vektör olan `v`'yi tanımlar ve sınıfın varsayılan kurucusunu çağırarak boş bir vektör oluşturur.
### Vektöre Eleman Ekleme
- **push_back:** Vektöre eleman eklemek için `push_back` üye fonksiyonu kullanılır.
    ```cpp
    v.push_back(10); // 10 değerini vektöre ekler
    ```
### Vektörün Boyut ve Kapasite Bilgisi
- **size():** Vektörün mevcut eleman sayısını döndürür.
    ```cpp
    int s = v.size(); // vektörde kaç eleman olduğunu döner
    ```
    
- **capacity():** Vektörün şu anda tahsis edilmiş olan bellek miktarını döndürür. Bu, tipik olarak `size`'dan büyüktür ve gerektiğinde otomatik olarak artırılır.
    ```cpp
    int c = v.capacity(); // vektörün kapasitesini döner
    ```
### Kapasiteyi Manuel Olarak Ayarlama
- **reserve:** Vektörün kapasitesini manuel olarak ayarlamak için `reserve` fonksiyonu kullanılır. Bu, verimliliğin kritik olduğu durumlarda faydalıdır.
    ```cpp
    v.reserve(32); // kapasiteyi 32 olarak ayarlar
    v.reserve(v.size() + 10); // kapasiteyi mevcut boyuttan 10 fazla olacak şekilde ayarlar
    ```
    
Bu özellikler, vektörlerin nasıl tanımlandığını, kullanıldığını ve verimli hale getirildiğini anlamanızı sağlar.
