*Links*: [[00 - Index|Index]]
*Date*: 05.11.2024
*Resources*: [name]()

---
# Pointers
- **Pointer Tanımı**: Pointer, bir değişkenin bellek adresini tutan bir değişkendir.
- **Bellek Yapısı**: Bilgisayar belleği, numaralandırılmış bellek konumlarına bölünmüştür. Her bellek konumunun bir adresi vardır ve bu adresler değişkenlerin yerini belirlemek için kullanılır.
- **Pointer Kullanımı**: Pointer'ları zaten kullanmış olabilirsiniz. Örneğin, call-by-reference (referans ile çağırma) parametrelerinde, bir fonksiyona bir değişkenin kendisi yerine, o değişkenin bellek adresi geçirilir. Bu sayede fonksiyon, değişkenin orijinal değerini değiştirebilir.

*Özetle, pointer'lar bellek adreslerini tutar ve bellek yönetiminde önemli bir rol oynar.*
## Pointer Variables
- **Pointer Türleri**: Pointer'lar belirli bir türe sahiptir. Yani, bir pointer belirli bir veri türünün adresini tutar.
- **Pointer Değişkeni**: Pointer'lar değişkenlerde saklanabilir, ancak int, double gibi temel veri türleri yerine, belirli bir türün pointer'ı olarak tanımlanırlar.
- **Pointer Tanımlama**: Pointer'lar diğer veri türleri gibi tanımlanır, ancak değişken adının önüne `*` eklenir. Bu, o değişkenin belirli bir türün pointer'ı olduğunu belirtir.
- **Örnek**:
  ```cpp
  double *p;
  ```
  Bu örnekte, `p` bir "double türüne işaret eden pointer" olarak tanımlanmıştır. Yani, `p` sadece double türündeki değişkenlerin adreslerini tutabilir.
- **Tür Uyumsuzluğu**: Pointer'lar sadece kendi türlerindeki değişkenlerin adreslerini tutabilirler. Farklı türdeki değişkenlerin adreslerini tutmak için tür dönüşümü (typecast) yapılabilir, ancak bu tehlikeli olabilir.

*Özetle, pointer'lar belirli bir veri türüne sahiptir ve sadece o türdeki değişkenlerin adreslerini tutabilirler.*

- **Pointer ve Adres**: Pointer, bir değişkenin bellek adresini tutan bir değişkendir. Bellek adresleri genellikle tamsayılar olarak temsil edilir.
- **Pointer ve Tamsayı Farkı**: Pointer'lar bellek adreslerini tutar, bu adresler tamsayılar gibi görünse de, pointer'lar tamsayı olarak kullanılmaz. Bu, programlama dillerinde bir soyutlama katmanı olarak kabul edilir. Yani, pointer'lar tamsayı gibi davranmazlar.
- **C++ ve Pointer Kullanımı**: C++ dilinde pointer'lar sadece adres olarak kullanılır. Bu, pointer'ların tamsayılar gibi matematiksel işlemlerde kullanılmasını engeller. Örneğin, bir pointer'ı doğrudan bir tamsayı ile toplamak veya çıkarmak genellikle anlamlı değildir ve bu tür işlemler dil tarafından kısıtlanır.

Özetle, pointer'lar bellek adreslerini tutar ve bu adresler tamsayılar gibi görünse de, C++ dilinde pointer'lar tamsayı olarak kullanılmaz. Bu, dilin pointer'ları adresler olarak ele almasını ve bellek yönetimini daha güvenli hale getirmesini sağlar.

### Pointing
- **Terminoloji**: Pointer'lar hakkında konuşurken "adres" yerine "işaret etme" terimi kullanılır.
- **Pointer Değişkeni**: Bir pointer değişkeni, sıradan bir değişkene "işaret eder".
- **Adres Konuşmasını Bırakmak**: "Adres" terimini kullanmamak, kavramın anlaşılmasını ve görselleştirilmesini daha kolay hale getirir.
- **Görselleştirme**: Bellek referanslarını daha net görmek için oklar kullanılır. Bu, pointer'ların hangi değişkenlere işaret ettiğini görselleştirmeyi sağlar.

Özetle, pointer'lar hakkında konuşurken "adres" yerine "işaret etme" terimini kullanmak, kavramın anlaşılmasını ve görselleştirilmesini kolaylaştırır. Bu sayede, pointer'ların bellek referanslarını daha net bir şekilde görebiliriz.

- **Pointer Tanımlama**:
  ```cpp
  int *p1, *p2, v1, v2;
  ```
  Bu satırda:
  - `p1` ve `p2` int türündeki değişkenlerin adreslerini tutan pointer'lardır.
  - `v1` ve `v2` ise sıradan int değişkenleridir.

- **Pointer Atama**:
  ```cpp
  p1 = &v1;
  ```
  Bu satırda:
  - `p1` pointer değişkeni, `v1` değişkeninin adresini tutacak şekilde ayarlanır.
  - `&` operatörü, bir değişkenin bellek adresini belirler.

- **Okuma Şekli**:
  - "p1 equals address of v1" (p1, v1'in adresine eşittir)
  - "p1 points to v1" (p1, v1'e işaret eder)

Özetle, `int *p1, *p2, v1, v2;` satırı pointer ve sıradan değişkenleri tanımlar. `p1 = &v1;` satırı ise `p1` pointer'ını `v1` değişkeninin adresine ayarlar. `&` operatörü, bir değişkenin adresini belirlemek için kullanılır.

### & Operator
- **"Address of" Operatörü**: `&` operatörü, bir değişkenin bellek adresini belirlemek için kullanılır.
- **Call-by-Reference Parametreleri**: `&` operatörü, call-by-reference (referans ile çağırma) parametrelerini belirtmek için de kullanılır.
- **İlişki**: Bu iki kullanım tesadüf değildir. Call-by-reference parametreleri, gerçek argümanın adresini geçirir. Bu sayede, fonksiyon orijinal değişken üzerinde işlem yapabilir.

Özetle, `&` operatörü hem bir değişkenin adresini belirlemek için hem de call-by-reference parametrelerini belirtmek için kullanılır. Bu iki kullanım, adreslerin fonksiyonlara geçirilmesiyle yakından ilişkilidir.

### The "new" Operator
- **Pointer'lar ve Değişkenler**: Pointer'lar değişkenlere işaret edebilir, bu nedenle standart bir tanımlayıcıya (identifier) ihtiyaç duymazlar.
- **Dinamik Bellek Tahsisi**: `new` operatörü ile dinamik olarak değişkenler oluşturulabilir.
- **Tanımlayıcı Olmadan Değişkenler**: `new` operatörü, tanımlayıcı olmadan değişkenler oluşturur ve sadece bir pointer ile bu değişkenlere erişilir.
- **Örnek**:
  ```cpp
  p1 = new int;
  ```
  Bu satırda:
  - `new int` ifadesi, yeni bir "isimsiz" int değişkeni oluşturur.
  - `p1` pointer'ı bu yeni değişkene işaret eder.
- **Erişim**: `*p1` ifadesi ile bu isimsiz değişkene erişilebilir ve tıpkı sıradan bir değişken gibi kullanılabilir.

- **Yeni Dinamik Değişken Oluşturma**: `new` operatörü, yeni bir dinamik değişken oluşturur ve bu yeni değişkene işaret eden bir pointer döner.
- **Sınıf Türleri**: Eğer tür bir sınıf türü ise, `new` operatörü ile oluşturulan yeni nesne için yapıcı (constructor) çağrılır.
- **Yapıcı ile Başlatma**: Farklı yapıcıları başlatıcı argümanlarla çağırabilirsiniz.
    ```cpp
    MyClass *mcPtr;
    mcPtr = new MyClass(32.0, 17);
    ```
    Bu satırda, `MyClass` sınıfının bir nesnesi oluşturulur ve `mcPtr` pointer'ı bu nesneye işaret eder. Yapıcı, `32.0` ve `17` argümanları ile çağrılır.
- **Sınıf Olmayan Türlerin Başlatılması**: Sınıf olmayan türler de başlatılabilir.
    ```cpp
    int *n;
    n = new int(17);  // *n değerini 17 olarak başlatır
    ```
    Bu satırda, yeni bir int değişkeni oluşturulur ve `n` pointer'ı bu değişkene işaret eder. Yeni int değişkeni `17` değeri ile başlatılır.

### Pointers and Functions
- Pointer'lar tam teşekküllü veri türleridir ve diğer veri türleri gibi kullanılabilirler. Fonksiyon parametresi olarak kullanılabilirler ve fonksiyonlardan döndürülebilirler. Örneğin:
	```cpp
	int* findOtherPointer(int* p);
	```
	Bu fonksiyon bildirimi, bir "int'e işaret eden pointer" parametresine sahiptir ve bir "int'e işaret eden pointer" döndürür. Bu, pointer'ların fonksiyonlarda nasıl kullanılabileceğini ve döndürülebileceğini gösterir. Pointer'lar, diğer veri türleri gibi esnek bir şekilde kullanılabilir ve programlama sırasında güçlü bir araç sağlar.

## Memory Management
- Heap, aynı zamanda "freestore" olarak da adlandırılır ve dinamik olarak tahsis edilen değişkenler için ayrılmış bir bellek alanıdır. Tüm yeni dinamik değişkenler, freestore'da bellek tüketir. Eğer çok fazla dinamik değişken oluşturulursa, freestore belleği tükenebilir. Bu durumda, gelecekteki `new` işlemleri başarısız olur çünkü freestore "dolu" olacaktır.
- Eski derleyicilerde, `new` operatörünün bellek tahsis edip edemediğini kontrol etmek için `NULL` döndürüp döndürmediği test edilirdi. Örneğin:

	```cpp
	int *p;
	p = new int;
	if (p == NULL)
	{
	    cout << "Error: Insufficient memory.\n";
	    exit(1);
	}
	```
	
	Bu kodda, `new int` ifadesi yeni bir int değişkeni oluşturmayı dener. Eğer bellek tahsisi başarısız olursa, `p` `NULL` olur. Bu durumda, hata mesajı yazdırılır ve program sonlandırılır. Eğer `new` başarılı olursa, program normal şekilde devam eder. Bu yöntem, bellek tahsis hatalarını yakalamak için kullanılırdı.
- Yeni derleyicilerde, `new` operatörü bellek tahsisi yapamazsa, program otomatik olarak sonlanır ve bir hata mesajı üretir. Ancak, `NULL` kontrolü yapmak hala iyi bir uygulamadır. Bu, bellek tahsis hatalarını daha iyi yönetmenize ve programın daha güvenilir olmasına yardımcı olabilir.
	```cpp
	int *p;
	try {
	    p = new int;
	} catch (std::bad_alloc& e) {
	    cout << "Error: Insufficient memory.\n";
	    exit(1);
	}
	```
	
	Bu kodda, `new` operatörü başarısız olursa, `std::bad_alloc` istisnası yakalanır ve uygun bir hata mesajı yazdırılarak program sonlandırılır. Bu, bellek tahsis hatalarını daha güvenli bir şekilde yönetmenin modern bir yoludur.

- Bellek yönetimi, uygulamadan uygulamaya değişiklik gösterebilir, ancak genellikle heap (freestore) oldukça büyüktür. Çoğu program tüm belleği kullanmaz, ancak bellek yönetimi hala iyi bir uygulamadır ve sağlam yazılım mühendisliği prensibidir. Bellek miktarı ne kadar büyük olursa olsun, sonuçta sınırlıdır.

- Bu nedenle, bellek yönetimi konusunda dikkatli olmak önemlidir. Dinamik bellek tahsisi yaparken bellek sızıntılarını önlemek ve bellek kullanımını optimize etmek, programların daha verimli ve güvenilir olmasını sağlar. Belleğin sınırlı olduğunu unutmamak, her zaman iyi bir yazılım mühendisliği pratiğidir.

### Delete operator
Dinamik belleği, artık ihtiyaç duyulmadığında serbest bırakmak önemlidir. Bu işlem, belleği freestore'a geri kazandırır. Örneğin:

```cpp
int *p;
p = new int(5);
// ... Bazı işlemler ...
delete p;
```

Bu kodda:
- `p = new int(5);` ifadesi, dinamik olarak bir int değişkeni oluşturur ve `p` pointer'ı bu değişkene işaret eder.
- `delete p;` ifadesi, `p` pointer'ının işaret ettiği dinamik belleği serbest bırakır. Bu, belleği freestore'a geri kazandırır ve bu bellek alanını başka işlemler için kullanılabilir hale getirir.

Belleği serbest bırakmak, bellek sızıntılarını önlemek ve bellek kullanımını optimize etmek için kritik öneme sahiptir. Bu işlem, dinamik olarak tahsis edilen belleği "yok eder" ve programın daha verimli çalışmasını sağlar.

### Dangling Pointer
`delete p;` ifadesi, dinamik belleği yok eder, ancak `p` hala o bellek alanına işaret eder. Bu duruma "dangling pointer" denir. Eğer `p` bu durumda dereference edilirse (`*p`), sonuçlar tahmin edilemez ve genellikle felaketle sonuçlanır.

Dangling pointer'ları önlemek için, `delete` işleminden sonra pointer'ı `NULL` olarak ayarlamak iyi bir uygulamadır:

```cpp
delete p;
p = NULL;
```

Bu şekilde, `p` artık geçersiz bir bellek alanına işaret etmez ve `NULL` kontrolü yaparak bu tür hatalardan kaçınabilirsiniz. Bu, bellek yönetiminde güvenliği artırır ve programın daha sağlam olmasını sağlar.

### Dynamic and Automatic Variables
Dinamik değişkenler, `new` operatörü ile oluşturulur ve program çalışırken yaratılır ve yok edilir. Örneğin:

```cpp
int *p = new int(5);
// ... Bazı işlemler ...
delete p;
```

Bu kodda, `p` dinamik olarak oluşturulan bir değişkene işaret eder ve `delete` ile serbest bırakılır.

Yerel değişkenler ise bir fonksiyon tanımı içinde bildirilir ve dinamik değildir. Örneğin:

```cpp
void myFunction() {
    int localVar = 10;
    // ... Bazı işlemler ...
}
```

Bu kodda, `localVar` fonksiyon çağrıldığında oluşturulur ve fonksiyon çağrısı tamamlandığında yok edilir. Bu tür değişkenlere genellikle "otomatik" değişkenler denir çünkü ömürleri ve özellikleri derleyici tarafından otomatik olarak yönetilir.

Özetle, dinamik değişkenler `new` operatörü ile oluşturulup yok edilirken, yerel (otomatik) değişkenler fonksiyon çağrıları sırasında otomatik olarak yönetilir.

### Define Pointer Types (Aliases)
Pointer türlerine isim verebilirsiniz, böylece diğer değişkenler gibi pointer'ları da tanımlayabilirsiniz. Bu, pointer tanımında `*` kullanımını ortadan kaldırır. Örneğin:

```cpp
typedef int* IntPtr;
```

Bu ifade, `int*` türüne bir takma ad (alias) tanımlar. Şimdi, aşağıdaki tanımlamaları düşünün:

```cpp
IntPtr p;
int *p;
```

Bu iki tanım eşdeğerdir. Her ikisi de `p` isimli bir `int` pointer'ı tanımlar. `typedef` kullanarak pointer türlerine isim vermek, kodun okunabilirliğini artırabilir ve pointer tanımlarını daha temiz hale getirebilir.

### Pitfall: Call-by-value Pointers
- Bir fonksiyonun işaretçi parametresini değiştirmesi, yalnızca o fonksiyonun yerel kopyasını değiştirir. Bu, fonksiyon dışında işaretçinin orijinal değerinin değişmediği anlamına gelir.

```c
#include <stdio.h>

void changePointer(int *ptr) {
    int localVar = 10;
    ptr = &localVar; // ptr now points to localVar, but this change is local to the function
}

int main() {
    int value = 5;
    int *ptr = &value;

    printf("Before: %d\n", *ptr); // Output: 5

    changePointer(ptr);

    printf("After: %d\n", *ptr); // Output: 5, ptr still points to value
    return 0;
}
```
1. main fonksiyonunda `value` değişkeni ve `ptr` işaretçisi tanımlanır. `ptr`, `value` değişkenini işaret eder.
2. `changePointer` fonksiyonu çağrıldığında, `ptr` işaretçisi fonksiyona kopyalanır.
3. Fonksiyon içinde `ptr` işaretçisi `localVar` değişkenini işaret edecek şekilde değiştirilir. Ancak bu değişiklik sadece fonksiyonun yerel kopyasında olur.
4. main fonksiyonuna geri dönüldüğünde, `ptr` hala `value` değişkenini işaret eder ve değeri değişmemiştir.

Bu örnek, işaretçi parametresinin değiştirilmesinin yalnızca yerel kopyayı etkilediğini ve orijinal işaretçinin değişmediğini göstermektedir.
# Dynamic Arrays
- Dizi değişkenleri aslında işaretçi değişkenleridir. Standart diziler sabit boyutludur ve boyutları programlama sırasında belirlenir. Dinamik diziler ise boyutları programlama sırasında belirlenmeyen, program çalışırken boyutu belirlenen dizilerdir. Standart diziler sabit bir bellek alanı kullanırken, dinamik diziler `malloc` gibi fonksiyonlarla bellekten yer ayırır ve `free` ile bu belleği serbest bırakır.
- Diziler bellekte ardışık adreslerde saklanır ve dizi değişkeni ilk indeksli değişkene "referans verir". Bu nedenle, dizi değişkeni bir tür işaretçi değişkenidir. Örneğin, `int a[10];` ve `int *p;` ifadelerinde, `a` ve `p` her ikisi de işaretçi değişkenleridir. `a` dizisinin adı, dizinin ilk elemanının adresini tutan bir işaretçidir.
- Önceki örneği hatırlayalım: `int a[10];` ve `typedef int* IntPtr;` ile `IntPtr p;` tanımlamaları yapılır. `a` ve `p` her ikisi de işaretçi değişkenleridir. `p = a;` ataması yasaldır ve `p` artık `a` dizisinin ilk elemanını işaret eder. Ancak `a = p;` ataması yasadışıdır çünkü dizi işaretçisi sabit bir işaretçidir ve başka bir adrese atanamaz.
- Dizi değişkeni `int a[10];` bir işaretçi değişkeninden daha fazlasıdır. `const int *` türündedir, çünkü dizi bellekte zaten ayrılmıştır ve `a` değişkeni her zaman bu belleğe işaret etmelidir. Bu işaretçi değiştirilemez. Buna karşılık, sıradan işaretçiler değiştirilebilir ve genellikle de değiştirilir.
- Dizilerin sınırlamaları vardır; boyutlarını önceden belirtmek gerekir ve bu boyut program çalışana kadar bilinmeyebilir. Bu durumda, genellikle ihtiyaç duyulacak maksimum boyut tahmin edilir. Bu bazen işe yarar, bazen ise yaramaz ve belleğin israfına yol açar. Dinamik diziler ise ihtiyaç duyuldukça büyüyebilir veya küçülebilir, bu da bellek kullanımını daha verimli hale getirir.
## Creating and Using
- `new` operatörünü kullanarak işaretçi değişkeni ile dinamik olarak bellek ayırabilirsiniz ve bu dizileri standart diziler gibi kullanabilirsiniz. Örneğin:
	```cpp
	typedef double * DoublePtr;
	DoublePtr d;
	d = new double[10];    // Köşeli parantez içinde boyut belirtilir
	```
	Bu, `double` türünde on elemanlı dinamik olarak ayrılmış bir dizi değişkeni `d` oluşturur.

- Dinamik olarak ayrılan bellek, çalışma zamanında serbest bırakılmalıdır. Örneğin:
	```cpp
	d = new double[10];
	// ... İşlem yapılıyor
	delete [] d; // Dinamik dizi için tüm belleği serbest bırakır
	d = NULL; // d hala orayı işaret ettiğinden, işaretçiyi NULL yapmalısınız
	```
	Bu, dinamik diziyi serbest bırakır ve `d` işaretçisini `NULL` yaparak bellek sızıntılarını önler.

- Fonksiyonların dönüş türü olarak dizi türü kullanılamaz. Örneğin:
	```cpp
	int [] someFunction();   // YASADIŞI!
	```
	Bunun yerine, dizinin temel türüne işaretçi döndürülmelidir:
	```cpp
	int* someFunction();  // YASAL!
	```
	Bu şekilde, fonksiyon bir diziye işaret eden bir işaretçi döndürebilir.
## Pointer Arithmetic
- İşaretçiler üzerinde aritmetik işlemler yapılabilir, bu "adres" aritmetiği olarak adlandırılır. Örneğin:
	```cpp
	typedef double* DoublePtr;
	DoublePtr d;
	d = new double[10];
	```
	- `d` işaretçisi `d[0]`'ın adresini içerir.
	- `d + 1`, `d[1]`'in adresine değerlendirilir.
	- `d + 2`, `d[2]`'nin adresine değerlendirilir.
	Bu, bu konumlardaki "adres" ile eşdeğerdir.

İşaretçi aritmetiğini kullanarak dizide indeksleme yapmadan dolaşabilirsiniz:
```cpp
for (int i = 0; i < arraySize; i++)
    cout << *(d + i) << " ";
```
Bu, şu ifadeye eşdeğerdir:
```cpp
for (int i = 0; i < arraySize; i++)
    cout << d[i] << " ";
```
İşaretçiler üzerinde yalnızca toplama ve çıkarma işlemleri yapılabilir. Çarpma ve bölme işlemleri yapılamaz. Ayrıca, işaretçiler üzerinde `++` ve `--` operatörleri kullanılabilir.

### Multidimensional Dynamic Arrays
"Dizilerin dizileri" (Multidimensional Dynamic Array) oluşturabiliriz. Tür tanımlamaları bunu daha net görmemize yardımcı olur:

```cpp
typedef int* IntArrayPtr;
IntArrayPtr *m = new IntArrayPtr[3]; // Üç işaretçiden oluşan bir dizi oluşturur
```

Her bir işaretçinin dört `int`'lik bir dizi ayırmasını sağlamak için:

```cpp
for (int i = 0; i < 3; i++)
    m[i] = new int[4];
```

Bu, üçe dört boyutunda dinamik bir dizi oluşturur.
# Classes, Pointers, Dynamic Arrays
### The -> Operator
- `->` operatörü, kısayol bir gösterimdir ve `*` (dereference) operatörü ile `.` (dot) operatörünü birleştirir. Bu, verilen işaretçinin işaret ettiği sınıfın üyesini belirtir. Örneğin:
	```cpp
	MyClass *p;
	p = new MyClass;
	p->grade = "A";   // Bu ifade, aşağıdaki ifadeye eşdeğerdir:
	(*p).grade = "A";
	```
	Bu, `p` işaretçisinin işaret ettiği `MyClass` nesnesinin `grade` üyesine erişir ve ona `"A"` değerini atar.
## The *this* pointer
Üye fonksiyon tanımlamaları, çağıran nesneye başvurmak için `this` işaretçisini kullanabilir. `this` işaretçisi otomatik olarak çağıran nesneyi işaret eder:
```cpp
class Simple
{
public:
    void showStuff() const;
private:
    int stuff;
};
```

Üye fonksiyonlar, `stuff` üyesine iki şekilde erişebilir:

```cpp
void Simple::showStuff() const {
    cout << stuff;         // Doğrudan erişim
    cout << this->stuff;   // this işaretçisi ile erişim
}
```

Her iki yöntem de `stuff` üyesine erişir ve aynı sonucu verir.

### Overloading Assignment Operator
Atama operatörü bir referans döndürdüğü için atama "zincirleri" mümkündür. Örneğin, `a = b = c;` ifadesi `a` ve `b`'yi `c`'ye eşitler. Operatör, zincirlerin çalışabilmesi için sol tarafındaki ile aynı türde bir değer döndürmelidir. Bu durumda `this` işaretçisi yardımcı olur.

Örneğin, bir sınıfın atama operatörünü aşırı yükleyelim:

```cpp
class MyClass {
public:
    MyClass& operator=(const MyClass& other) {
        if (this != &other) { // Kendine atamayı önlemek için
            // Üye değişkenlerin kopyalanması
            this->value = other.value;
        }
        return *this; // this işaretçisini dereference ederek kendisini döndürür
    }

private:
    int value;
};
```

Bu şekilde, `a = b = c;` ifadesi çalışabilir çünkü `operator=` fonksiyonu `*this` döndürerek atama zincirlerinin çalışmasını sağlar.

## Shallow and Deep Copy

### Shallow Copy (Yüzeysel Kopya)
Yüzeysel kopya, yalnızca üye değişkenlerin içeriklerini kopyalar. Varsayılan atama operatörleri ve kopya yapıcılar yüzeysel kopya yapar.

```cpp
class Shallow {
public:
    int* data;

    Shallow(int value) {
        data = new int(value);
    }

    // Varsayılan kopya yapıcı ve atama operatörü yüzeysel kopya yapar
};

int main() {
    Shallow obj1(5);
    Shallow obj2 = obj1; // Yüzeysel kopya
    return 0;
}
```

### Deep Copy (Derin Kopya)
Derin kopya, işaretçi değişkenlerinin işaret ettiği verileri de kopyalar. Bu durumda, kendi atama operatörünüzü ve kopya yapıcınızı yazmanız gerekir.

```cpp
class Deep {
public:
    int* data;

    Deep(int value) {
        data = new int(value);
    }

    // Derin kopya için kopya yapıcı
    Deep(const Deep& other) {
        data = new int(*other.data);
    }

    // Derin kopya için atama operatörü
    Deep& operator=(const Deep& other) {
        if (this == &other) return *this; // Kendine atamayı önlemek için
        delete data; // Eski belleği serbest bırak
        data = new int(*other.data); // Yeni bellek ayır ve kopyala
        return *this;
    }

    ~Deep() {
        delete data; // Belleği serbest bırak
    }
};

int main() {
    Deep obj1(5);
    Deep obj2 = obj1; // Derin kopya
    return 0;
}
```

#### Açıklama
- **Yüzeysel Kopya**: `Shallow` sınıfında, varsayılan kopya yapıcı ve atama operatörü yalnızca işaretçi değişkenin adresini kopyalar.
- **Derin Kopya**: `Deep` sınıfında, kopya yapıcı ve atama operatörü işaretçi değişkenin işaret ettiği verileri de kopyalar. Bu, dinamik belleği yönetmek için gereklidir.

## Destructor gereklidir!
Dinamik olarak ayrılmış değişkenler, `delete` edilene kadar bellekte kalır. Eğer işaretçiler yalnızca özel üye verileriyse, gerçek verileri dinamik olarak ayırırlar. Bu durumda, nesne yok edildiğinde bu belleği serbest bırakmanın bir yolu olmalıdır. Cevap: yıkıcı (destructor)!

#### Örnek
```cpp
class MyClass {
public:
    MyClass(int size) {
        data = new int[size]; // Dinamik olarak bellek ayır
    }

    ~MyClass() {
        delete[] data; // Belleği serbest bırak
    }

private:
    int* data; // Dinamik olarak ayrılmış veriyi işaret eden işaretçi
};

int main() {
    MyClass obj(10); // Nesne oluşturulur ve bellek ayrılır
    // Nesne yok edildiğinde yıkıcı çağrılır ve bellek serbest bırakılır
    return 0;
}
```

### Açıklama

- **Constructor**: Nesne oluşturulduğunda dinamik olarak bellek ayırır.
- **Destructor**: Nesne yok edildiğinde dinamik olarak ayrılmış belleği serbest bırakır.

Bu şekilde, dinamik olarak ayrılmış belleğin yönetimi sağlanır ve bellek sızıntıları önlenir.
## Dectructors, copy constructors
### Destructor
Yapıcıların (constructor) tersi olan yıkıcılar (destructor), bir nesne kapsam dışına çıktığında otomatik olarak çağrılır. Varsayılan yıkıcı, yalnızca sıradan değişkenleri kaldırır, dinamik değişkenleri kaldırmaz. Yıkıcı, yapıcı gibi tanımlanır, sadece başına `~` eklenir.

```cpp
class MyClass {
public:
    MyClass(int size) {
        data = new int[size]; // Dinamik olarak bellek ayır
    }

    ~MyClass() {
        delete[] data; // Dinamik belleği serbest bırak
    }

private:
    int* data; // Dinamik olarak ayrılmış veriyi işaret eden işaretçi
};

int main() {
    MyClass obj(10); // Nesne oluşturulur ve bellek ayrılır
    // Nesne yok edildiğinde yıkıcı çağrılır ve bellek serbest bırakılır
    return 0;
}
```

- **Yapıcı (Constructor)**: Nesne oluşturulduğunda dinamik olarak bellek ayırır.
- **Yıkıcı (Destructor)**: Nesne yok edildiğinde dinamik olarak ayrılmış belleği serbest bırakır.

Bu şekilde, dinamik olarak ayrılmış belleğin yönetimi sağlanır ve bellek sızıntıları önlenir.

### Copy Constructor
Yıkıcılar (destructor) ve kopya yapıcılar (copy constructor) otomatik olarak çağrılır. Kopya yapıcı, aşağıdaki durumlarda otomatik olarak çağrılır:

1. Bir sınıf nesnesi başka bir nesneye atanarak oluşturulduğunda.
2. Bir fonksiyon sınıf türünde bir nesne döndürdüğünde.
3. Bir sınıf türündeki argüman, call-by-value parametresi olarak kullanıldığında.

Bu durumlar, nesnenin geçici bir kopyasını gerektirir ve kopya yapıcı bu kopyayı oluşturur. Varsayılan kopya yapıcı, varsayılan atama operatörü gibi üye değişkenleri tek tek kopyalar. Ancak, işaretçiler söz konusu olduğunda, kendi kopya yapıcınızı yazmanız gerekir.

```cpp
class MyClass {
public:
    MyClass(int size) {
        data = new int[size]; // Dinamik olarak bellek ayır
        length = size;
    }

    // Kopya yapıcı
    MyClass(const MyClass& other) {
        length = other.length;
        data = new int[length];
        for (int i = 0; i < length; i++) {
            data[i] = other.data[i];
        }
    }

    ~MyClass() {
        delete[] data; // Dinamik belleği serbest bırak
    }

private:
    int* data; // Dinamik olarak ayrılmış veriyi işaret eden işaretçi
    int length;
};

int main() {
    MyClass obj1(10); // Nesne oluşturulur ve bellek ayrılır
    MyClass obj2 = obj1; // Kopya yapıcı çağrılır
    return 0;
}
```

- **Kopya Yapıcı (Copy Constructor)**: `MyClass(const MyClass& other)` kopya yapıcısı, `other` nesnesinin verilerini derinlemesine kopyalar. Bu, işaretçilerin işaret ettiği verileri de kopyalar.
- **Yıkıcı (Destructor)**: `~MyClass()` yıkıcısı, dinamik olarak ayrılmış belleği serbest bırakır.

Bu şekilde, dinamik bellek yönetimi sağlanır ve derin kopyalama gerçekleştirilir.