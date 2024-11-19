*Links*: [[00 - Index]]
*Date*: 19.11.2024
*Resources*: [name]()

---
# I/O Streams
Stream'ler, program giriş ve çıkışını sağlayan özel nesnelerdir. Dosya I/O (Input/Output) işlemleri için kullanılırlar ve kalıtım (inheritance) kullanırlar. Dosya I/O işlemleri çok kullanışlı olduğu için burada ele alınmaktadır, ancak kalıtım konusuna 14. bölümde değinilecektir.

Dosya I/O işlemleri, programların dosyalardan veri okumasını ve dosyalara veri yazmasını sağlar. Bu işlemler genellikle `ifstream` (input file stream) ve `ofstream` (output file stream) sınıfları kullanılarak gerçekleştirilir.

Örnek:
```cpp
#include <iostream>
#include <fstream>

int main() {
    // Dosyaya yazma
    // Çıkış için ofstream nesnesi kullanarak dosyayı açma
    std::ofstream outFile("example.txt");
    if (outFile.is_open()) {
        outFile << "Hello, file!" << std::endl;
        outFile.close();
    } else {
        std::cerr << "Unable to open file for writing." << std::endl;
    }

    // Dosyadan okuma
    // Giriş için ifstream nesnesi kullanarak dosyayı açma
    std::ifstream inFile("example.txt");
    if (inFile.is_open()) {
        std::string line;
        while (std::getline(inFile, line)) {
            std::cout << line << std::endl;
        }
        inFile.close();
    } else {
        std::cerr << "Unable to open file for reading." << std::endl;
    }

    return 0;
}
```

- Bir karakter akışı olarak tanımlanan stream'ler, giriş ve çıkış işlemlerini sağlar.

**Input stream**:
- Programın içine doğru akan karakter akışıdır.
- Klavyeden gelebilir.
- Dosyadan gelebilir.

**Output stream**:
- Programdan dışarı doğru akan karakter akışıdır.
- Ekrana gidebilir.
- Dosyaya gidebilir.

Örnek:
```cpp
#include <iostream>
#include <fstream>

int main() {
    // Klavyeden giriş (input stream)
    std::string userInput;
    std::cout << "Enter some text: ";
    std::getline(std::cin, userInput); // std::cin klavyeden giriş sağlar
    std::cout << "You entered: " << userInput << std::endl;

    // Dosyaya yazma (output stream)
    std::ofstream outFile("output.txt");
    if (outFile.is_open()) {
        outFile << userInput << std::endl; // std::ofstream dosyaya yazma sağlar
        outFile.close();
    } else {
        std::cerr << "Unable to open file for writing." << std::endl;
    }

    // Dosyadan okuma (input stream)
    std::ifstream inFile("output.txt");
    if (inFile.is_open()) {
        std::string fileContent;
        while (std::getline(inFile, fileContent)) {
            std::cout << "File content: " << fileContent << std::endl; // std::ifstream dosyadan okuma sağlar
        }
        inFile.close();
    } else {
        std::cerr << "Unable to open file for reading." << std::endl;
    }

    return 0;
}
```

- Verilen programda bir dosyadan okuma ve bir dosyaya yazma işlemleri şu şekilde yapılabilir:
```cpp
#include <iostream>
#include <fstream>

int main() {
    // Dosyadan okuma için input stream tanımlama
    std::ifstream inStream("input.txt");
    if (!inStream) {
        std::cerr << "Unable to open input file." << std::endl;
        return 1;
    }

    int theNumber;
    inStream >> theNumber; // Stream'den değer okuma ve theNumber'a atama
    inStream.close();

    // Dosyaya yazma için output stream tanımlama
    std::ofstream outStream("output.txt");
    if (!outStream) {
        std::cerr << "Unable to open output file." << std::endl;
        return 1;
    }

    outStream << "theNumber is " << theNumber << std::endl; // Değeri stream'e yazma, bu dosyaya gider
    outStream.close();

    return 0;
}
```

Bu örnekte:
- `inStream` adlı input stream, `input.txt` dosyasından veri okur ve bu değeri `theNumber` değişkenine atar.
- `outStream` adlı output stream, `output.txt` dosyasına "theNumber is " ve `theNumber` değişkeninin değerini yazar.


## File I/O
Stream'ler diğer sınıf değişkenleri gibi tanımlanmalıdır. Daha sonra dosyaya "bağlanmaları" gerekir. Bu işlem, `open` üye fonksiyonu kullanılarak yapılır ve buna "dosyayı açma" denir. Tam dosya yolunu da belirtebilirsiniz.

Örnek:
```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    // ifstream ve ofstream nesnelerini tanımlama
    std::ifstream inStream;
    std::ofstream outStream;

    // Dosyayı açma
    inStream.open("infile.txt"); // Giriş dosyasını açma
    if (!inStream) {
        std::cerr << "Unable to open input file." << std::endl;
        return 1;
    }

    outStream.open("outfile.txt"); // Çıkış dosyasını açma
    if (!outStream) {
        std::cerr << "Unable to open output file." << std::endl;
        return 1;
    }

    // Dosyadan okuma ve dosyaya yazma işlemleri
    std::string line;
    while (std::getline(inStream, line)) {
        outStream << line << std::endl; // Okunan satırı çıkış dosyasına yazma
    }

    // Dosyaları kapatma
    inStream.close();
    outStream.close();

    return 0;
}
```

Bu örnekte:
- `ifstream` nesnesi `inStream` ve `ofstream` nesnesi `outStream` olarak tanımlanır.
- `inStream.open("infile.txt")` ifadesi ile giriş dosyası açılır.
- `outStream.open("outfile.txt")` ifadesi ile çıkış dosyası açılır.
- Dosyadan okuma ve dosyaya yazma işlemleri gerçekleştirilir.
- Dosyalar `close` üye fonksiyonu ile kapatılır.

Tam dosya yolunu belirtmek isterseniz, `open` fonksiyonuna tam dosya yolunu geçirebilirsiniz:
```cpp
inStream.open("/path/to/your/infile.txt");
outStream.open("/path/to/your/outfile.txt");
```

Bu şekilde, dosyaları açarak giriş ve çıkış işlemlerini gerçekleştirebilirsiniz.

- Stream'ler bir kez tanımlandıktan sonra normal şekilde kullanılabilirler. İşte giriş ve çıkış stream'lerinin nasıl kullanılacağına dair bir örnek:

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    // ifstream ve ofstream nesnelerini tanımlama
    std::ifstream inStream;
    std::ofstream outStream;

    // Dosyayı açma
    inStream.open("infile.txt"); // Giriş dosyasını açma
    if (!inStream) {
        std::cerr << "Unable to open input file." << std::endl;
        return 1;
    }

    outStream.open("outfile.txt"); // Çıkış dosyasını açma
    if (!outStream) {
        std::cerr << "Unable to open output file." << std::endl;
        return 1;
    }

    // Dosyadan okuma
    int oneNumber, anotherNumber;
    inStream >> oneNumber >> anotherNumber;

    // Dosyaya yazma
    outStream << "oneNumber = " << oneNumber
              << " anotherNumber = " << anotherNumber;

    // Dosyaları kapatma
    inStream.close();
    outStream.close();

    return 0;
}
```

Bu örnekte:
- `ifstream` nesnesi `inStream` ve `ofstream` nesnesi `outStream` olarak tanımlanır.
- `inStream.open("infile.txt")` ifadesi ile giriş dosyası açılır.
- `outStream.open("outfile.txt")` ifadesi ile çıkış dosyası açılır.
- `inStream` kullanılarak `oneNumber` ve `anotherNumber` değişkenlerine dosyadan veri okunur.
- `outStream` kullanılarak bu değişkenlerin değerleri dosyaya yazılır.
- Dosyalar `close` üye fonksiyonu ile kapatılır.

Bu şekilde, dosyaları açtıktan sonra stream'leri normal şekilde kullanarak veri okuma ve yazma işlemlerini gerçekleştirebilirsiniz.

- Çıktı genellikle "buffered" olarak işlenir, yani dosyaya yazılmadan önce geçici olarak depolanır ve gruplar halinde yazılır. Bazen, yazma işlemini zorlamak gerekebilir. Bunun için `flush` üye fonksiyonu kullanılır. Bu fonksiyon, tüm buffered çıktıyı fiziksel olarak dosyaya yazar. Dosyayı kapatmak (`close`) otomatik olarak `flush()` fonksiyonunu çağırır.
- Dosyayı ekleme modunda açmak için `ios::app` kullanabilirsiniz: `outStream.open("important.txt", std::ios::app); // Ekleme modunda aç`
- Dosya adını tanımlama sırasında belirtebilirsiniz. Bu, dosya adını yapıcıya (constructor) argüman olarak geçer. İki yöntem de eşdeğerdir:
```cpp
	// Birinci yöntem: Dosyayı open ile açma
    std::ifstream inStream;
    inStream.open("infile.txt");

    // İkinci yöntem: Dosya adını yapıcıya geçme
    std::ifstream inStream2("infile.txt");
```
## Character I/O
`cin` ve `cout` ile yapılan karakter I/O işlemleri dosyalar için de aynı şekilde çalışır. Üye fonksiyonlar aynı şekilde kullanılır:

- `get`
- `getline`
- `put`
- `putback`
- `peek`
- `ignore`

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ifstream inStream("input.txt");
    std::ofstream outStream("output.txt");

    if (inStream.fail() || outStream.fail()) {
        std::cerr << "File open failed.\n";
        return 1;
    }

    char ch;
    while (inStream.get(ch)) {
        outStream.put(ch); // Karakteri dosyaya yazma
    }

    inStream.close();
    outStream.close();
    return 0;
}
```
Bu örnekte, `get` ve `put` fonksiyonları dosya I/O işlemleri için kullanılır.

- Dosyanın sonuna kadar işlem yapmak için döngü kullanabilirsiniz. Dosyanın sonunu test etmek için iki yöntem vardır. `eof()` üye fonksiyonu bunlardan biridir. İşte bir örnek:

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ifstream inStream("input.txt");
    if (inStream.fail()) {
        std::cerr << "File open failed.\n";
        return 1;
    }

    char next;
    inStream.get(next);
    while (!inStream.eof()) {
        std::cout << next;
        inStream.get(next);
    }

    inStream.close();
    return 0;
}
```

Bu örnekte:
- `inStream.get(next)` ile karakter okunur.
- `while (!inStream.eof())` döngüsü dosyanın sonuna kadar devam eder.
- Her karakter `std::cout` ile ekrana yazdırılır.
# Tools for Stream I/O
Dosya stream'leri üzerinde "sihirli formül"ü kullanarak sayıları belirli bir formatta yazdıran bir örnek:

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ofstream outStream("output.txt");
    if (outStream.fail()) {
        std::cerr << "File open failed.\n";
        return 1;
    }

    // "Sihirli formül"ü uygulama
    outStream.setf(std::ios::fixed);
    outStream.setf(std::ios::showpoint);
    outStream.precision(2);
    
	// Genişlik ayarları ile sütunlar oluşturma
    outStream.width(10);
    outStream << number1 << std::endl;

    double number = 12.5234;
    outStream << number << std::endl;

    outStream.close();
    return 0;
}
```

Bu örnekte:
- `output.txt` dosyası açılır.
- "Sihirli formül" uygulanarak sayılar belirli bir formatta yazdırılır.
- `number` değişkeni dosyaya "12.52" formatında yazdırılır.
- Dosya kapatılır.


`setf()` üye fonksiyonu çıktı bayraklarının durumunu ayarlar. Tüm çıktı stream'leri `setf()` üye fonksiyonuna sahiptir. Bayraklar, `ios` sınıfında sabitler olarak tanımlanmıştır ve `<iostream>` kütüphanesinde, `std` namespace'inde bulunur.
## File names as input
## Formatting output, flag settings
# Stream Hierarchies
## Preview of inheritance
# Random Access to Files