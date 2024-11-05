*Links*: [[00 - Index|Index]]
*Date*: 05.11.2024
*Resources*: [name]()

---
# An Array Type for Strings
### İki Tür String Tipi
#### C-Strings
- **Tanım**: C-strings, karakter dizileridir ve `char` türünde bir dizi olarak temsil edilir.
- **Sonlandırma**: C-strings, null karakter (`\0`) ile sonlandırılır.
- **Köken**: C dilinden miras alınmıştır ve "eski" bir yöntem olarak kabul edilir.
#### Örnek: C-Strings
```cpp
#include <iostream>

int main() {
    char cstr[] = "Hello, World!";
    std::cout << cstr << std::endl; // C-string yazdırma
    return 0;
}
```

#### `string` Sınıfı
- **Tanım**: C++'da `string` sınıfı, daha modern ve kullanımı kolay bir string tipidir.
- **Şablonlar (Templates)**: `string` sınıfı, şablonlar kullanılarak tanımlanmıştır ve daha fazla işlevsellik sunar.
- **Avantajlar**: Bellek yönetimi, string işlemleri ve güvenlik açısından daha avantajlıdır.
#### Örnek: `string` Sınıfı
```cpp
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello, World!";
    std::cout << str << std::endl; // string yazdırma
    return 0;
}
```
### Özet
- **C-Strings**: `char` türünde bir dizi olarak temsil edilir ve null karakter (`\0`) ile sonlandırılır. C dilinden miras alınmıştır.
- **`string` Sınıfı**: C++'da daha modern ve kullanımı kolay bir string tipidir. Şablonlar kullanılarak tanımlanmıştır ve daha fazla işlevsellik sunar.

Bu iki string tipi, C++'da farklı ihtiyaçlara göre kullanılabilir. C-strings daha düşük seviyeli ve manuel bellek yönetimi gerektirirken, `string` sınıfı daha yüksek seviyeli ve kullanımı kolaydır.
## C-Strings
- **C-Strings**: `char` türünde bir dizi olarak temsil edilir.
- **Her İndeksli Değişken**: Dizinin her bir elemanı bir karakteri temsil eder.
- **Ekstra Karakter**: Dizinin sonunda bir null karakter (`\0`) bulunur. Bu karakter, stringin sonunu belirtir ve "null karakter" olarak adlandırılır.
#### Örnek: C-Strings
```cpp
#include <iostream>

int main() {
    // C-string tanımlama
    char cstr[] = "Hello";

    // C-string yazdırma
    std::cout << cstr << std::endl; // "Hello"

    // C-string'in her karakterini yazdırma
    for (int i = 0; cstr[i] != '\0'; ++i) {
        std::cout << cstr[i] << ' ';
    }
    std::cout << std::endl; // H e l l o

    return 0;
}
```

Bu örnekte:
- `"Hello"` stringi, `char` dizisi olarak tanımlanır ve C-string olarak saklanır.
- Dizinin sonunda `\0` karakteri bulunur, bu da stringin sonunu belirtir.
- `for` döngüsü kullanılarak stringin her karakteri yazdırılır.
### Özet
- **C-Strings**: `char` türünde bir dizi olarak temsil edilir ve her indeksli değişken bir karakteri temsil eder.
- **Null Karakter (`\0`)**: Dizinin sonunda bulunur ve stringin sonunu belirtir.
- **Örnek Kullanım**: `"Hello"` stringi, C-string olarak saklanır ve yazdırılır.

C-strings, C dilinden miras alınmış bir yöntemdir ve düşük seviyeli string işlemleri için kullanılır. Bu yöntem, manuel bellek yönetimi gerektirir ve dikkatli kullanılmalıdır.

```cpp
#include <iostream>

int main() {
    // 10 karakterlik bir dizi tanımlama
    char s[10];

    // Diziyi bir string ile doldurma
    s[0] = 'H';
    s[1] = 'e';
    s[2] = 'l';
    s[3] = 'l';
    s[4] = 'o';
    s[5] = '\0'; // Null karakter ile sonlandırma

    // C-string yazdırma
    std::cout << s << std::endl; // "Hello"

    // Dizinin her karakterini yazdırma
    for (int i = 0; s[i] != '\0'; ++i) {
        std::cout << s[i] << ' ';
    }
    std::cout << std::endl; // H e l l o

    return 0;
}
```
Bu örnekte:
- `char s[10];` ifadesi, 10 karakterlik bir dizi tanımlar.
- Dizinin sonunu belirtmek için null karakter (`\0`) kullanılır.
- Dizinin her karakteri yazdırılır.

### C-Strings'in Başlatılması
#### Başlatma ve Boyut Belirleme
1. **Dizi Boyutunu Belirterek Başlatma**:
    - `char myMessage[20] = "Hi there.";`
    - Bu ifade, `myMessage` dizisini 20 karakterlik bir alan olarak tanımlar ve `"Hi there."` stringini bu diziye yerleştirir.
    - Dizinin geri kalanı boş kalır ve stringin sonunda otomatik olarak null karakter (`\0`) eklenir.
2. **Dizi Boyutunu Belirtmeden Başlatma**:
    - `char shortString[] = "abc";`
    - Bu ifade, `shortString` dizisini `"abc"` stringinin uzunluğuna göre otomatik olarak boyutlandırır.
    - Dizinin boyutu, stringin uzunluğundan bir fazla olur (null karakter (`\0`) için).
#### Yanlış Başlatma
- `char shortString[] = {"a", "b", "c"};`
    - Bu ifade, karakter dizisi yerine karakterlerin ayrı ayrı elemanlar olarak tanımlandığı bir dizi oluşturur ve C-string olarak kullanılmaz.
### C-Strings ve İndeksli Değişkenlere Erişim
#### C-Strings'in Tanımı
- **C-Strings**: `char` türünde bir dizi olarak temsil edilir.
- **Dizi Elemanları**: Her bir eleman bir karakteri temsil eder ve dizinin sonunda null karakter (`\0`) bulunur.
```cpp
#include <iostream>

int main() {
    // C-string tanımlama
    char ourString[5] = "Hi";

    // İndeksli değişkenlere erişim
    std::cout << "ourString[0]: " << ourString[0] << std::endl; // H
    std::cout << "ourString[1]: " << ourString[1] << std::endl; // i
    std::cout << "ourString[2]: " << static_cast<int>(ourString[2]) << std::endl; // 0 (null karakter)
    std::cout << "ourString[3]: " << static_cast<int>(ourString[3]) << std::endl; // bilinmiyor
    std::cout << "ourString[4]: " << static_cast<int>(ourString[4]) << std::endl; // bilinmiyor

    return 0;
}
```
Bu örnekte:
- `char ourString[5] = "Hi";` ifadesi, 5 karakterlik bir dizi tanımlar ve `"Hi"` stringini bu diziye yerleştirir.
- `ourString[0]` karakteri `"H"`'dir.
- `ourString[1]` karakteri `"i"`'dir.
- `ourString[2]` karakteri null karakter (`\0`)'dir.
- `ourString[3]` ve `ourString[4]` karakterleri bilinmiyor ve belirsizdir.

#### İndeksli Değişkenlerin Manipülasyonu
- C-strings'in indeksli değişkenlerine erişebilir ve bu değişkenleri manipüle edebilirsiniz.
- Ancak, null karakterin (`\0`) üzerine yazmak tehlikelidir çünkü bu, stringin sonunu belirtir ve stringin C-string gibi davranmasını engeller.
```cpp
char happyString[7] = "DoBeDo";
happyString[6] = 'Z'; // Null karakterin üzerine yazma
```
- Bu, stringin sonunu belirtmek için kullanılan null karakterin üzerine yazıldığı anlamına gelir ve string artık C-string gibi davranmaz. Bu da beklenmedik sonuçlara yol açabilir.
### Özet
- **C-Strings**: `char` dizisi olarak temsil edilir ve null karakter (`\0`) ile sonlandırılır.
- **Manipülasyon**: İndeksli değişkenler manipüle edilebilir, ancak null karakterin üzerine yazmak stringin doğru çalışmamasına neden olur.
# Character Manipulation Tools
C-strings, `char` dizisi olarak tanımlanır ve herhangi bir ek C++ kütüphanesi gerektirmez. Bu özellik, standart C++'ın bir parçasıdır.

C-strings manipülasyonları için `<cstring>` kütüphanesi gereklidir. Bu kütüphane, C-strings ile çeşitli işlemler yapmanızı sağlayan fonksiyonlar içerir.

Örnek fonksiyonlar:

- `strcpy`: Bir C-string'i başka bir C-string'e kopyalar.
- `strlen`: Bir C-string'in uzunluğunu döndürür.
- `strcmp`: İki C-string'i karşılaştırır.
- `strcat`: Bir C-string'i başka bir C-string'in sonuna ekler.

Özetle, C-strings tanımlamak için ek kütüphane gerekmez, ancak manipülasyonlar için `<cstring>` kütüphanesi kullanılır.

- C-strings, diğer değişkenler gibi atanamaz veya karşılaştırılamaz.
```cpp
char aString[10];
aString = "Hello"; // GEÇERSİZ!
```
- C-strings için sadece tanımlama sırasında `=` kullanılabilir. Atama için kütüphane fonksiyonu kullanılmalıdır: `strcpy(aString, "Hello");`. Bu fonksiyon `<cstring>` kütüphanesinde bulunur ve `aString` değerini `"Hello"` yapar. (Boyut kontrolü yapmaz, bu yüzden dikkat programcıya aittir. Diğer dizilerde olduğu gibi.)
- C-strings, `==` operatörü ile karşılaştırılamaz. Karşılaştırma için `strcmp` fonksiyonu kullanılmalıdır. `strcmp` fonksiyonu `<cstring>` kütüphanesinde bulunur ve iki string'i karşılaştırır. Ör: `strcmp(aString, anotherString)`
- `strlen` fonksiyonu, string'in uzunluğunu döndürür. Null karakter (`\0`) dahil edilmez.
- `strcat()` fonksiyonu, "string concatenate" (string birleştirme) işlemi yapar. Ör: `char stringVar[20] = "The rain"; strcat(stringVar, "in Spain");` Bu işlemden sonra `stringVar` şu değeri içerir: "The rainin Spain"
- C-strings bir dizidir, bu yüzden C-string parametresi de bir dizi parametresidir. C-strings fonksiyonlara geçirildiğinde, alıcı fonksiyon tarafından değiştirilebilir. Tüm dizilerde olduğu gibi, genellikle boyut da gönderilir. Ancak, fonksiyon C-string'i değiştirmeyecekse, boyut gerekli değildir çünkü fonksiyon `\0` karakterini kullanarak stringin sonunu bulabilir.
- C-string argümanlarını korumak için `const` anahtar kelimesi kullanılabilir.
Örnek:
```cpp
void printCString(const char* str) {
    while (*str != '\0') {
        std::cout << *str;
        str++;
    }
}

int main() {
    char myString[] = "Hello, World!";
    printCString(myString); // "Hello, World!" yazdırır
    return 0;
}
```

- C-strings, `<<` operatörü ile çıktılanabilir.
- C-strings, `>>` operatörü ile girdilenebilir. Ancak bazı sorunlar vardır:
	- Boşluk karakterleri (tab, boşluk, satır sonu) "ayırıcı" olarak kullanılır.
	- Girdi okuma, ayırıcıya geldiğinde durur.
	- C-string'in boyutu, girilen stringi tutacak kadar büyük olmalıdır.
	- C++ bu tür sorunlar hakkında uyarı vermez.
- Bir C-string'e tüm satırı almak için `getline()` fonksiyonunu kullanabilirsiniz. Bu fonksiyon, boşluk karakterlerini de dahil ederek tüm satırı okur.
```cpp
#include <iostream>

int main() {
    char a[80];
    std::cout << "Enter input: ";
    std::cin.getline(a, 80); // destination, limit
    std::cout << a << "END OF OUTPUT\n";
    return 0;
}
// INPUT: Enter input: Do be do to you!
// OUTPUT: Do be do to you!END OF OUTPUT
```
- Komut satırından çalıştırılan programlar, argümanlar alabilir. Örneğin, UNIX shell veya DOS komut istemcisi gibi. Ör:
```cpp
#include <iostream>

int main(int argc, char* argv[]) {
    std::cout << "Number of arguments: " << argc << std::endl;
    for (int i = 0; i < argc; ++i) {
        std::cout << "Argument " << i << ": " << argv[i] << std::endl;
    }
    return 0;
}
// INPUT: COPY C:\FOO.TXT D:\FOO2.TXT
// COPY programı, bu girdileri işleyerek dosyaları kopyalamalıdır.
```
## Character I/O
- Girdi ve çıktı verileri, karakter verisi olarak işlenir. Örneğin, sayı 10 çıktılanırken "1" ve "0" karakterleri olarak yazdırılır. Bu dönüşüm otomatik olarak yapılır ve düşük seviyeli araçlar kullanılır.
- Biz de aynı düşük seviyeli araçları kullanabiliriz. Ör:
```cpp
#include <iostream>

int main() {
    int number = 10;
    std::cout << number << std::endl; // "10" olarak yazdırır

    char str[3];
    std::sprintf(str, "%d", number); // Sayıyı karakter dizisine dönüştürür
    std::cout << str << std::endl; // "10" olarak yazdırır

    return 0;
}
```
- Bu örnekte:
	- `std::cout`, sayıyı otomatik olarak karakterlere dönüştürür.
	- `std::sprintf`, sayıyı karakter dizisine dönüştürmek için düşük seviyeli bir araçtır.
## get, put, member functions
- `cin.get()` fonksiyonu, bir seferde bir karakter okur. Bu, `cin` nesnesinin bir üye fonksiyonudur.
- `cout.put()` fonksiyonu, bir seferde bir karakter çıktılar. Bu, `cout` nesnesinin bir üye fonksiyonudur. Ör: `std::cout.put('a'); // Ekrana "a" harfini yazdırır`
## putback, peek, ignore
- `putback()` : Bir karakter okunduktan sonra, bu karakteri geri koymak için kullanılır. ("Karakteri geri koymak" ifadesi, `putback()` fonksiyonunun okunan bir karakteri girdi akışına geri yerleştirmesi anlamına gelir. Bu, sanki karakter hiç okunmamış gibi davranılmasını sağlar. Bu, bir karakteri okuduktan sonra tekrar kullanmanız gerektiğinde faydalıdır.)
- `peek()` : Bir sonraki karakteri döndürür, ancak bu karakteri girdi akışında bırakır.
- `ignore()` : Belirtilen karaktere kadar veya belirtilen sayıda karakteri atlamak için kullanılır.

# Standard Class String
- `string` değişkenleri ve ifadeleri, basit türler gibi işlenir. Atama, karşılaştırma ve ekleme işlemleri yapılabilir.
- C-string ifadeleri, otomatik olarak `string` türüne dönüştürülür.
- `string` türü de diğer basit türler gibi işlenir. `cin` kullanarak `string` değişkenlerine değer atayabilirsiniz. Ancak, `cin` operatörü boşluk karakterlerini ayırıcı olarak kullanır ve boşluk karakterine kadar olan kısmı okur.
- `getline()` fonksiyonu, `string` türü ile tam satırları okumak için kullanılabilir. Bu, C-string'lerde kullanılan `getline()` fonksiyonuna benzer şekilde çalışır. Ama parametreleri farklıdır: `string line; getline(cin, line);`
- `getline()` fonksiyonu, belirli bir ayırıcı karaktere kadar olan girişi de okuyabilir. Ör: `getline(cin, line, '?'); // "?" karakterine kadar oku`
- `getline()` fonksiyonu bir referans döndürür, bu nedenle zincirleme işlemler yapılabilir. Ör: `getline(cin, s1) >> s2; // İlk satırı s1'e, sonraki kelimeyi s2'ye alır`

```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    string s1, s2, s3;

    // Atama
    s1 = "Hello";
    s2 = " Mom!";

    // Birleştirme (Concatenation)
    s3 = s1 + s2; // s3 = "Hello Mom!"

    // Doğrudan atama
    s3 = "Hello Mom!"; // C-string "Hello Mom!" otomatik olarak string türüne dönüştürülür

    // Sonuçları yazdırma
    cout << "s1: " << s1 << endl;
    cout << "s2: " << s2 << endl;
    cout << "s3: " << s3 << endl;

    return 0;
}
```
Bu örnekte:
- `s1` ve `s2` string değişkenlerine değerler atanır.
- `s3 = s1 + s2;` ifadesi, `s1` ve `s2` stringlerini birleştirir ve `s3` değişkenine atar.
- `s3 = "Hello Mom!";` ifadesi, C-string `"Hello Mom!"` ifadesini otomatik olarak `string` türüne dönüştürür ve `s3` değişkenine atar.
## String Processing
C++'daki `string` sınıfı, C-strings ile aynı işlemleri ve daha fazlasını sunar. Standart `string` sınıfının 100'den fazla üye fonksiyonu vardır. İşte bazı önemli üye fonksiyonlar:
### Önemli Üye Fonksiyonlar
- `.length()`: String değişkeninin uzunluğunu döndürür.
  ```cpp
  string str = "Hello";
  cout << str.length(); // 5
  ```

- `.at(i)`: Belirtilen `i` konumundaki karakterin referansını döndürür.
  ```cpp
  string str = "Hello";
  cout << str.at(1); // 'e'
  ```
### Örnek Kullanım
```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    string str = "Hello, World!";

    // .length() kullanımı
    cout << "Length: " << str.length() << endl; // 13

    // .at(i) kullanımı
    cout << "Character at position 1: " << str.at(1) << endl; // 'e'

    return 0;
}
```
Bu örnekte:
- `str.length()` ifadesi, stringin uzunluğunu döndürür.
- `str.at(1)` ifadesi, stringin 1. konumundaki karakteri döndürür.
### Özet
- `string` sınıfı, C-strings ile aynı işlemleri ve daha fazlasını sunar.
- `.length()` fonksiyonu, stringin uzunluğunu döndürür.
- `.at(i)` fonksiyonu, belirtilen konumdaki karakterin referansını döndürür.

Bu fonksiyonlar, `string` sınıfının sunduğu birçok işlevden sadece birkaçıdır. `string` sınıfı, string işlemlerini daha kolay ve esnek hale getirir.

- C++'da, C-string'den `string` nesnesine otomatik tür dönüşümleri yapılabilir. Ancak, `string` nesnesinden C-string'e otomatik dönüşüm yapılamaz.
```cpp
char aCString[] = "My C-string";
string stringVar;
stringVar = aCString; // Geçerli ve uygun
```

***Örnek: `string` Nesnesinden C-string'e Dönüşüm***
```cpp
char aCString[50];
string stringVar = "My string";

// Geçersiz: aCString = stringVar; // Bu otomatik dönüşüm yapılamaz

// Geçerli: Açık dönüşüm kullanarak
strcpy(aCString, stringVar.c_str());
```
Açıklama:
- `stringVar = aCString;` ifadesi, C-string'den `string` nesnesine otomatik dönüşüm yapar ve geçerlidir.
- `aCString = stringVar;` ifadesi geçersizdir çünkü `string` nesnesinden C-string'e otomatik dönüşüm yapılamaz.
- `strcpy(aCString, stringVar.c_str());` ifadesi, `string` nesnesini C-string'e dönüştürmek için açık dönüşüm kullanır. `c_str()` fonksiyonu, `string` nesnesinin C-string temsilini döndürür.
### Özet
- C-string'den `string` nesnesine otomatik dönüşüm yapılabilir.
- `string` nesnesinden C-string'e otomatik dönüşüm yapılamaz.
- `string` nesnesini C-string'e dönüştürmek için `strcpy` ve `c_str()` fonksiyonu kullanılır.