*Links*: [[00 - Index]]
*Date*: 19.11.2024
*Resources*: [name]()

---
# Seperate Compilation
- Program parçaları genellikle ayrı dosyalarda tutulur, ayrı ayrı derlenir ve program çalışmadan önce linked edilir. Class tanımları, kullanım programlarından ayrı tutulur ve bir class kütüphanesi oluşturulur. Bu kütüphane, birçok farklı program tarafından yeniden kullanılabilir ve önceden tanımlanmış kütüphaneler gibi işlev görür.
- Class bağımsızlığı, class tanımı ve implementasyonunun ayrı tutulması anlamına gelir. Class tanımı/specification, "interface" olarak adlandırılır. Class implementasyonu ise ayrı bir dosyada bulunur. Bu iki dosya ayrı tutulur. Eğer implementasyon değişirse, sadece o dosyanın değiştirilmesi yeterlidir. Class specification değişmek zorunda değildir ve "user" programlarının da değişmesine gerek kalmaz.
## Encapsulation reviewed
- Encapsulation prensibi, bir class'ın programcı tarafından nasıl kullanıldığını, class'ın implementasyon detaylarından ayırmayı amaçlar. Bu prensip, "tam" bir ayrım sağlar. Implementasyonda yapılan bir değişiklik, diğer programlar üzerinde hiçbir etki yaratmaz. Bu, temel bir OOP (Object-Oriented Programming) prensibidir.
- Ayrımı sağlamak için bazı kurallar vardır. Tüm member değişkenleri private olmalıdır. Temel class operasyonları ise public member fonksiyonları, friend veya ordinary fonksiyonlar ve overloaded operatörler olmalıdır. Class tanımı ve prototipleri bir arada gruplandırılmalıdır ve bu "interface" olarak adlandırılır. Class implementasyonu, class kullanıcılarına erişilemez hale getirilmelidir.
## Header and Implementation Files
- Interface dosyası, class tanımını ve fonksiyon ile operatör deklarasyonlarını/prototiplerini içerir. Kullanıcılar bu dosyayı "görür". Bu, ayrı bir derleme birimidir. Implementasyon dosyası ise member fonksiyon tanımlarını içerir ve bu da ayrı bir derleme birimidir.
- Class interface her zaman bir header dosyasında bulunur ve .h isimlendirme kuralı kullanılır. Class'ı kullanan programlar bu dosyayı "include" eder, örneğin `#include "myclass.h"`. Tırnak işaretleri, header dosyasını sizin yazdığınızı ve çalışma dizininizde bulunduğunu belirtir. Kütüphane include'larını hatırlayın, örneğin `<iostream>`. Köşeli parantezler, önceden tanımlanmış bir kütüphane header dosyasını belirtir ve bu dosya kütüphane dizininde bulunur.
- Class implementasyonu .cpp dosyasında bulunur. Genellikle interface dosyası ve implementasyon dosyasına aynı isim verilir, örneğin myclass.h ve myclass.cpp. Tüm class'ın member fonksiyonları burada tanımlanır. Implementasyon dosyası, class'ın header dosyasını `#include` etmelidir. Genel olarak, .cpp dosyaları çalıştırılabilir kod içerir, örneğin fonksiyon tanımları ve main() fonksiyonu.
- Class header dosyası, implementasyon dosyası ve program dosyası (genellikle "application file" veya "driver file" olarak adlandırılır) tarafından `#include` edilir. Dosyaların organizasyonu sisteme bağlıdır. Tipik bir IDE, "project" veya "workspace" kavramına sahiptir. Implementasyon dosyaları burada "combined" edilir ve header dosyaları hala `#include` edilir.
- Header dosyaları genellikle birden fazla kez include edilir, örneğin class interface hem class implementasyonu hem de program dosyası tarafından include edilir. Ancak, header dosyaları sadece bir kez derlenmelidir. Hangi dosyada `#include` ifadesinin ilk görüleceği garanti edilemez. Bu durumu yönetmek için preprocessor kullanılır ve derleyiciye header dosyasını sadece bir kez include etmesini söyleriz. Bunu sağlamak için header dosyasının başına ve sonuna aşağıdaki gibi preprocessor direktifleri eklenir:
	```cpp
	#ifndef MYCLASS_H
	#define MYCLASS_H
	
	// Class definition here
	
	#endif // MYCLASS_H
	```
- Kütüphaneler sadece class'lar için değildir. İlgili fonksiyonlar da kütüphanelerde bulunabilir. Fonksiyon prototipleri header dosyasında, tanımları ise implementasyon dosyasında yer alır. Diğer tür tanımları, örneğin `struct`lar ve basit `typedef`ler header dosyasında bulunur. Sabit (constant) deklarasyonları da header dosyasında yer alır.
# Namespaces
- Namespace, isim tanımlarının bir koleksiyonudur ve class tanımları ile değişken deklarasyonlarını içerir. Programlar birçok class ve fonksiyon kullanır ve bunlar genellikle aynı isimlere sahip olabilir. Namespace'ler bu durumu yönetir. Namespace'ler "açık" veya "kapalı" olabilir. Eğer isimler çakışma ihtimali taşıyorsa, namespace'leri kullanarak bu çakışmaları önleyebilirsiniz.
## Using Directives
- `using namespace std;` ifadesi, std namespace içindeki tüm tanımlamaları kullanılabilir hale getirir. Ancak, bunu kullanmak istemeyebileceğiniz durumlar vardır. Örneğin, `cout` ve `cin` gibi std namespace içindeki tanımlamaların standart olmayan anlamlara sahip olmasına neden olabilir. Belki `cout` ve `cin`'i yeniden tanımlamanız gerekebilir. Aynı şekilde, diğer tanımlamaları da yeniden tanımlayabilirsiniz. Bu nedenle, namespace çakışmalarını önlemek için dikkatli kullanılmalıdır.
- `namespace std`'u kullandığımızda bu, birçok standart kütüphane dosyasında tanımlanan tüm isimleri içerir. Örneğin, `#include <iostream>` ifadesi, tüm isim tanımlarını (`cin`, `cout`, vb.) std namespace içine yerleştirir. Program bu isimleri doğrudan bilmez. Programın bu isimlere erişebilmesi için bu namespace'i belirtmesi gerekir.
- Tüm kodlar bir namespace içinde yer alır. Eğer belirtilmezse, global namespace içinde bulunur. `using` direktifine gerek yoktur çünkü global namespace her zaman kullanılabilir durumdadır. Bu, implied "automatic" using direktifi anlamına gelir.
- Birden fazla namespace kullanılabilir, örneğin global ve std namespace'leri genellikle kullanılır. Ancak, aynı isim her iki namespace'de de tanımlanmışsa bir hata oluşur. Yine de her iki namespace'i de kullanabilirsiniz, ancak hangi namespace'in hangi zamanda kullanılacağını belirtmeniz gerekir. Örneğin:

```cpp
std::cout << "Using std namespace" << std::endl;
::cout << "Using global namespace" << std::endl; // Eğer global namespace'de cout tanımlıysa
```
- Eğer NS1 ve NS2 namespace'lerinde farklı şekilde tanımlanmış `myFunction()` fonksiyonları varsa, `using` direktifi blok kapsamına sahiptir. Bu, her blok içinde hangi namespace'in kullanılacağını belirlemenizi sağlar. Örneğin:

```cpp
namespace NS1 {
    void myFunction() {
        // NS1'e özgü implementasyon
    }
}

namespace NS2 {
    void myFunction() {
        // NS2'ye özgü implementasyon
    }
}

int main() {
    {
        using namespace NS1;
        myFunction(); // NS1::myFunction() çağrılır
    }
    {
        using namespace NS2;
        myFunction(); // NS2::myFunction() çağrılır
    }
    return 0;
}
```
- Namespace gruplaması kullanarak, belirli bir kod bloğunu bir namespace içine yerleştirebilirsiniz. Bu, tüm tanımlamaların belirli bir namespace içinde toplanmasını sağlar. Daha sonra bu namespace'i kullanılabilir hale getirebilirsiniz. Örneğin:

```cpp
namespace Name_Space_Name {
    // Some_Code
    void myFunction() {
        // Fonksiyon tanımı
    }
    int myVariable;
}

// Namespace'i kullanılabilir hale getirme
using namespace Name_Space_Name;

int main() {
    myFunction(); // Name_Space_Name::myFunction() çağrılır
    myVariable = 10; // Name_Space_Name::myVariable kullanılır
    return 0;
}
```

Bu şekilde, `Some_Code` içinde tanımlanan tüm isimler `Name_Space_Name` namespace'ine yerleştirilir ve `using namespace Name_Space_Name` ifadesi ile kullanılabilir hale getirilir.

- Fonksiyon bildirimi ve tanımı şu şekilde yapılabilir:
	Fonksiyon bildirimi:
	```cpp
	namespace Space1 {
	    void greeting();
	}
	```
	
	Fonksiyon tanımı:
	```cpp
	namespace Space1 {
	    void greeting() {
	        std::cout << "Hello from namespace Space1.\n";
	    }
	}
	```
	
	Bu şekilde, `greeting` fonksiyonu `Space1` namespace'i içinde bildirilir ve tanımlanır.

- Namespace içindeki bireysel isimleri belirtebilirsiniz. Örneğin, NS1 ve NS2 namespace'leri varsa ve her birinde fun1() ve fun2() fonksiyonları tanımlıysa, aşağıdaki gibi belirli isimleri kullanabilirsiniz:
	
	```cpp
	namespace NS1 {
	    void fun1() {
	        std::cout << "NS1::fun1" << std::endl;
	    }
	    void fun2() {
	        std::cout << "NS1::fun2" << std::endl;
	    }
	}
	
	namespace NS2 {
	    void fun1() {
	        std::cout << "NS2::fun1" << std::endl;
	    }
	    void fun2() {
	        std::cout << "NS2::fun2" << std::endl;
	    }
	}
	
	int main() {
	    using NS1::fun1; // NS1'den fun1'i kullan
	    using NS2::fun2; // NS2'den fun2'yi kullan
	
	    fun1(); // NS1::fun1 çağrılır
	    fun2(); // NS2::fun2 çağrılır
	
	    // Eğer NS1::fun2 veya NS2::fun1 çağrılmak istenirse, namespace belirtilmelidir
	    NS1::fun2();
	    NS2::fun1();
	
	    return 0;
	}
	```
	
	Bu şekilde, `using` direktifi ile belirli isimleri belirterek hangi namespace'den hangi fonksiyonun kullanılacağını açıkça belirtebilirsiniz.
	
```cpp
	using NS1::fun1; // Sadece NS1 içindeki fun1'i kullanılabilir hale getirir
	using namespace NS1; // NS1 içindeki tüm isimleri kullanılabilir hale getirir
```
## Qualifying Names
- İsimlerin nereden geldiğini belirlemek için "qualifier" ve scope-resolution operatörünü kullanabilirsiniz. Bu, sadece bir kez veya birkaç kez kullanmayı düşündüğünüzde özellikle yararlıdır.
	Örneğin:
	```cpp
	NS1::fun1(); // fun1'in NS1 namespace'inden geldiğini belirtir
	```
	
	Bu yöntem, parametreler için de özellikle kullanışlıdır:
	```cpp
	int getInput(std::istream& inputStream);
	```
	
	Bu durumda, `istream` türü `std` namespace'inde bulunduğundan, `std::istream` kullanarak `using` direktifi veya deklarasyonuna ihtiyaç duymadan belirtebilirsiniz. Bu, kodun daha okunabilir ve anlaşılır olmasını sağlar.
- Namespace isimlerinin benzersiz olmasını sağlamak için, genellikle benzersiz bir dize eklemek iyi bir uygulamadır. Örneğin, soyadınızı veya başka bir benzersiz tanımlayıcıyı kullanabilirsiniz. Bu, aynı isimde başka namespace'lerin olma olasılığını azaltır. Özellikle aynı program için birden fazla programcı namespace yazıyorsa, isimlerin farklı olması gerekir. Aksi takdirde, aynı kapsamda aynı ismin birden fazla tanımı hata ile sonuçlanır.
## Unnamed Namespaces
Derleme birimi, bir dosya ve o dosyada `#include` edilen tüm dosyalar olarak tanımlanır. Her derleme biriminin isimsiz bir namespace'i vardır. Bu namespace, aynı şekilde yazılır ancak bir adı yoktur. Bu durumda, tüm isimler derleme birimine yerel olur. İsimsiz namespace, şeyleri "yerel" tutmak için kullanılır. İsimsiz namespace'in kapsamı, derleme birimidir.

Örnek:
```cpp
namespace {
    void localFunction() {
        std::cout << "This is a local function." << std::endl;
    }

    int localVariable = 42;
}

int main() {
    localFunction(); // İsimsiz namespace içindeki fonksiyon çağrılır
    std::cout << localVariable << std::endl; // İsimsiz namespace içindeki değişken kullanılır
    return 0;
}
```

Bu şekilde, `localFunction` ve `localVariable` sadece bu derleme biriminde yerel olur ve başka yerlerde çakışma olmaz.

**Global namespace ve isimsiz namespace aynı değildir.**

**Global namespace**:
- Hiçbir namespace gruplaması yoktur.
- Global kapsamda bulunur.
- Tüm dosyalarda erişilebilir.

Örnek:
```cpp
void globalFunction() {
    std::cout << "This is a global function." << std::endl;
}
```

**Unnamed namespace**:
- Namespace gruplaması vardır, ancak bir adı yoktur.
- Yerel kapsamda bulunur.
- Sadece bulunduğu derleme biriminde erişilebilir.

Örnek:
```cpp
namespace {
    void localFunction() {
        std::cout << "This is a local function in an unnamed namespace." << std::endl;
    }
}
```

Bu şekilde, isimsiz namespace ile global namespace arasındaki farkı görebilirsiniz. İsimsiz namespace, isimleri sadece bulunduğu derleme biriminde yerel tutar, global namespace ise tüm dosyalarda erişilebilir.
## Hiding Helping Functions
Yardımcı fonksiyonları gizlemek için iki yol vardır:

1. **Private member function yapmak**:
   - Eğer fonksiyon doğal olarak çağıran nesneyi alıyorsa, bu fonksiyonu class'ın private member function'ı olarak tanımlayabilirsiniz.

2. **Class implementasyonunun isimsiz namespace'ine yerleştirmek**:
   - Eğer fonksiyonun çağıran bir nesneye ihtiyacı yoksa, bu fonksiyonu class implementasyonunun isimsiz namespace'ine yerleştirebilirsiniz. Bu, daha temiz kod sağlar çünkü nitelendiricilere gerek kalmaz.

Örnekler:

**Private member function**:
```cpp
class MyClass {
private:
    void helperFunction() {
        // Yardımcı fonksiyonun tanımı
    }
public:
    void publicFunction() {
        helperFunction(); // Private member function çağrılır
    }
};
```

**Isimsiz namespace içinde fonksiyon**:
```cpp
namespace {
    void helperFunction() {
        // Yardımcı fonksiyonun tanımı
    }
}

class MyClass {
public:
    void publicFunction() {
        helperFunction(); // Isimsiz namespace içindeki fonksiyon çağrılır
    }
};
```

Bu yöntemler, yardımcı fonksiyonları gizleyerek kodunuzu daha temiz ve yönetilebilir hale getirir.
## Nested Namespaces
Namespace'leri iç içe yerleştirmek yasaldır. Örneğin:

```cpp
namespace S1 {
    namespace S2 {
        void sample() {
            // Fonksiyon tanımı
        }
    }
}
```

Bu durumda, isimleri iki kez nitelendirmeniz gerekir:

```cpp
S1::S2::sample();
```

Bu şekilde, `sample` fonksiyonunun `S1` namespace'i içindeki `S2` namespace'inde tanımlandığını belirtmiş olursunuz.