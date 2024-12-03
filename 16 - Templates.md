*Links*: [[00 - Index]]
*Date*: 03.12.2024
*Resources*: [name]()

---
C++ şablonları, fonksiyonlar ve sınıflar için çok "genel" tanımlar yapılmasına olanak tanır. Tür isimleri, gerçek türler yerine "parametreler" olarak kullanılır. Kesin tanım, compile zamanında belirlenir. 

Örnek bir C++ şablon fonksiyonu:

```cpp
template <typename T>
T add(T a, T b) {
    return a + b;
}
```

Bu şablon fonksiyonu, `int`, `float` veya herhangi bir türdeki iki değeri toplamak için kullanılabilir.
# Function Templates
`swapValues` fonksiyonunu hatırlayalım:

```cpp
void swapValues(int& var1, int& var2)
{
    int temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}
```

Bu fonksiyon sadece `int` türündeki değişkenler için geçerlidir. Ancak, kod herhangi bir tür için çalışabilir. Bunu şablon kullanarak genelleştirebiliriz:

```cpp
template <typename T>
void swapValues(T& var1, T& var2)
{
    T temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}
```

Bu şekilde, `swapValues` fonksiyonu herhangi bir türdeki değişkenler için kullanılabilir.

## Overloading with Templates
Fonksiyonu `char` türü için aşırı yükleyebiliriz:

```cpp
void swapValues(char& var1, char& var2)
{
    char temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}
```

Ancak dikkat edin, kod neredeyse aynıdır! Tek fark, üç yerde kullanılan türdür. Bu nedenle, şablon kullanarak bu kodu genelleştirebiliriz:

```cpp
template <typename T>
void swapValues(T& var1, T& var2)
{
    T temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}
```

Bu şekilde, `swapValues` fonksiyonu herhangi bir türdeki değişkenler için kullanılabilir ve kod tekrarı önlenir.

## Template Prefix
Hatırlayalım:

```cpp
template<class T>
```

Bu kullanımda, "class" "tür" veya "sınıflandırma" anlamına gelir. Bu, kelimenin diğer "bilinen" kullanımı olan "class" ile karıştırılabilir. C++ burada "class" anahtar kelimesi yerine "typename" anahtar kelimesine de izin verir. Ancak, çoğu kişi yine de "class" kullanır.

Örneğin, aşağıdaki iki şablon tanımı eşdeğerdir:

```cpp
template<class T>
void swapValues(T& var1, T& var2)
{
    T temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}

template<typename T>
void swapValues(T& var1, T& var2)
{
    T temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}
```

Her iki kullanım da geçerlidir ve aynı işlevselliği sağlar.

`T`, herhangi bir tür ile değiştirilebilir. Bu tür, önceden tanımlanmış bir tür veya kullanıcı tanımlı bir tür (örneğin, bir C++ sınıf türü) olabilir. Fonksiyon tanımının gövdesinde, `T` diğer türler gibi kullanılır. Not: `T` yerine başka bir şey de kullanılabilir, ancak `T` geleneksel kullanımdır.

Örneğin:

```cpp
template<class T>
void swapValues(T& var1, T& var2)
{
    T temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}
```

Bu şablon fonksiyonunda, `T` herhangi bir tür olabilir ve fonksiyon gövdesinde diğer türler gibi kullanılır.
## Function Template Definition
`swapValues()` fonksiyon şablonu aslında büyük bir "tanımlar koleksiyonu" gibidir! Her olası tür için bir tanım vardır. Derleyici, yalnızca gerektiğinde tanımları oluşturur. Ancak, sanki tüm türler için tanımlamışsınız gibi çalışır. Bir tanım yazarsınız ve bu, ihtiyaç duyulabilecek tüm türler için çalışır.

Örneğin:

```cpp
template<class T>
void swapValues(T& var1, T& var2)
{
    T temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}
```

Bu tek tanım, `int`, `char`, `float`, kullanıcı tanımlı sınıflar gibi herhangi bir tür için çalışabilir. Derleyici, yalnızca belirli bir tür için bu fonksiyon çağrıldığında gerekli tanımı oluşturur.

## Calling a Function Template
Aşağıdaki çağrıyı düşünelim:

```cpp
swapValues(int1, int2);
```

C++ derleyicisi, şablonu kullanarak iki `int` parametresi için fonksiyon tanımını "oluşturur". Aynı şekilde, diğer tüm türler için de geçerlidir. Çağrıda herhangi bir "özel" bir şey yapmanıza gerek yoktur. Gerekli tanım otomatik olarak oluşturulur.

Örneğin:

```cpp
int a = 5, b = 10;
swapValues(a, b); // int türü için tanım oluşturulur

char c1 = 'x', c2 = 'y';
swapValues(c1, c2); // char türü için tanım oluşturulur

std::string s1 = "hello", s2 = "world";
swapValues(s1, s2); // std::string türü için tanım oluşturulur
```

Her çağrıda, derleyici gerekli tür için `swapValues` fonksiyonunun tanımını otomatik olarak oluşturur.

Başka bir örnekle:
```cpp
template<class T>
void showStuff(int stuff1, T stuff2, T stuff3);
```

Fonksiyon tanımı:
```cpp
template<class T>
void showStuff(int stuff1, T stuff2, T stuff3)
{
    std::cout << stuff1 << std::endl
              << stuff2 << std::endl
              << stuff3 << std::endl;
}
```

Bu şablon fonksiyon, `int` türünde bir `stuff1` ve `T` türünde iki `stuff2` ve `stuff3` parametresi alır. `T` herhangi bir tür olabilir. Fonksiyon, bu parametreleri `cout` ile ekrana yazdırır.

Fonksiyon çağrısını düşünelim:
```cpp
showStuff(2, 3.3, 4.4);
```

Derleyici, fonksiyon tanımını oluşturur ve `T`'yi `double` ile değiştirir. Çünkü ikinci parametre `double` türündedir. Bu çağrı, aşağıdaki çıktıyı gösterir:
```
2
3.3
4.4
```

Derleyici tarafından oluşturulan fonksiyon tanımı şu şekilde olur:

```cpp
void showStuff(int stuff1, double stuff2, double stuff3)
{
    std::cout << stuff1 << std::endl
              << stuff2 << std::endl
              << stuff3 << std::endl;
}
```

Bu sayede, `showStuff` fonksiyonu çağrıldığında doğru türlerle çalışır ve beklenen çıktıyı üretir.

## Compiler Complications
Fonksiyon bildirimleri ve tanımları genellikle ayrı dosyalarda bulunur. Ancak, şablonlar için bu çoğu derleyicide desteklenmez! Şablon fonksiyon tanımını çağrıldığı dosyada yerleştirmek en güvenlisidir. Birçok derleyici, tanımın önce görünmesini gerektirir. Bu nedenle, genellikle tüm şablon tanımlarını `#include` ederiz.

Örneğin, `showStuff` şablon fonksiyonunu kullanmak için:

```cpp
// showStuff.h
#ifndef SHOWSTUFF_H
#define SHOWSTUFF_H

#include <iostream>

template<class T>
void showStuff(int stuff1, T stuff2, T stuff3)
{
    std::cout << stuff1 << std::endl
              << stuff2 << std::endl
              << stuff3 << std::endl;
}

#endif // SHOWSTUFF_H
```

Ve bu şablonu kullanmak istediğimiz dosyada:

```cpp
// main.cpp
#include "showStuff.h"

int main() {
    showStuff(2, 3.3, 4.4);
    return 0;
}
```

Bu şekilde, şablon fonksiyon tanımı çağrıldığı dosyada yer alır ve derleyici tarafından doğru şekilde işlenir.

Derleyicinizin özel gereksinimlerini kontrol edin. Bazıları özel seçeneklerin ayarlanmasını gerektirir, bazıları ise şablon tanımlarının diğer dosya öğelerine göre özel bir düzenlemesini gerektirir. En kullanışlı şablon program düzeni:

1. Şablon tanımını kullanıldığı dosyada bulundurun.
2. Şablon tanımının tüm kullanımlardan önce geldiğinden emin olun.
3. Gerekirse, şablon tanımını `#include` edebilirsiniz.

Örneğin:

```cpp
// showStuff.h
#ifndef SHOWSTUFF_H
#define SHOWSTUFF_H

#include <iostream>

template<class T>
void showStuff(int stuff1, T stuff2, T stuff3)
{
    std::cout << stuff1 << std::endl
              << stuff2 << std::endl
              << stuff3 << std::endl;
}

#endif // SHOWSTUFF_H
```

Ve bu şablonu kullanmak istediğimiz dosyada:

```cpp
// main.cpp
#include "showStuff.h"

int main() {
    showStuff(2, 3.3, 4.4);
    return 0;
}
```

Bu düzen, şablon fonksiyon tanımının doğru şekilde işlenmesini sağlar ve derleyici tarafından doğru şekilde kullanılmasını garanti eder.

## Multiple Type Parameters

Şu şekilde olabilir:
```cpp
template<class T1, class T2>
```

Bu tipik değildir, genellikle yalnızca bir "değiştirilebilir" türe ihtiyaç duyulur. Kullanılmayan şablon parametrelerine sahip olamazsınız. Her biri tanımda "kullanılmalıdır", aksi takdirde hata oluşur!

Örneğin, iki tür parametresi kullanan geçerli bir şablon fonksiyonu:

```cpp
template<class T1, class T2>
void showStuff(T1 stuff1, T2 stuff2)
{
    std::cout << stuff1 << std::endl
              << stuff2 << std::endl;
}
```

Bu şablon fonksiyonunda, hem `T1` hem de `T2` parametreleri kullanılır. Kullanılmayan bir parametre olması durumunda derleyici hata verecektir. Örneğin:

```cpp
template<class T1, class T2>
void showStuff(T1 stuff1)
{
    std::cout << stuff1 << std::endl;
    // T2 kullanılmıyor, bu hata oluşturur
}
```

Bu durumda, `T2` kullanılmadığı için derleyici hata verecektir.

## Algorithm Abstraction
Şablonları uygulamaktan bahsederken, algoritmaları "genel" bir şekilde ifade ederiz:

- Algoritma, herhangi bir türdeki değişkenlere uygulanabilir.
- Önemsiz detayları göz ardı ederiz.
- Algoritmanın esas kısımlarına odaklanırız.

Fonksiyon şablonları, C++'ın algoritma soyutlamasını desteklemesinin bir yoludur.

Örneğin, bir sıralama algoritmasını şablon kullanarak genelleştirebiliriz:

```cpp
template<class T>
void sort(T arr[], int size)
{
    for (int i = 0; i < size - 1; ++i)
    {
        for (int j = 0; j < size - i - 1; ++j)
        {
            if (arr[j] > arr[j + 1])
            {
                T temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```

Bu `sort` fonksiyonu, `int`, `float`, `double` veya kullanıcı tanımlı türler gibi herhangi bir türdeki diziyi sıralamak için kullanılabilir. Bu şekilde, algoritmayı genel bir şekilde ifade eder ve türden bağımsız hale getiririz.

## Defining Template Strategies

Fonksiyonu normal şekilde geliştirin:
1. Gerçek veri türlerini kullanarak fonksiyonu yazın.
2. "Sıradan" fonksiyonu tamamen hata ayıklayın.
3. Ardından şablona dönüştürün.
4. Gerekli yerlerde tür isimlerini tür parametresi ile değiştirin.

Avantajları:
- "Somut" durumu çözmek daha kolaydır.
- Algoritma ile ilgilenirsiniz, şablon sözdizimi ile değil.

Örneğin, önce `int` türü için bir `swap` fonksiyonu yazalım:

```cpp
void swap(int& a, int& b)
{
    int temp = a;
    a = b;
    b = temp;
}
```

Bu fonksiyonu tamamen hata ayıklayın ve çalıştığından emin olun. Ardından, şablona dönüştürün:

```cpp
template<class T>
void swap(T& a, T& b)
{
    T temp = a;
    a = b;
    b = temp;
}
```

Bu şekilde, önce somut bir durum üzerinde çalışarak algoritmayı doğru bir şekilde uygularsınız ve ardından şablona dönüştürerek türden bağımsız hale getirirsiniz.

## Inappropriate Types in Templates

Şablonda, kodun "anlamlı" olduğu herhangi bir türü kullanabilirsiniz. Kodun uygun şekilde davranması gerekir. Örneğin, `swapValues()` şablon fonksiyonu, atama operatörünün tanımlı olmadığı bir tür için kullanılamaz. Örnek:
```cpp
int a[10], b[10];
swapValues(a, b); // Hata: Diziler atanamaz!
```

Diziler atanamaz, bu nedenle `swapValues` şablon fonksiyonu dizilerle çalışmaz. Şablon fonksiyonunun çalışması için kullanılan türün atama operatörünü desteklemesi gerekir.

Örneğin, `swapValues` şablon fonksiyonu:
```cpp
template<class T>
void swapValues(T& var1, T& var2)
{
    T temp = var1;
    var1 = var2;
    var2 = temp;
}
```

Bu fonksiyon, atama operatörünü destekleyen türler için çalışır. Ancak, diziler gibi atama operatörünü desteklemeyen türler için çalışmaz.
# Class Templates
Sınıfları da "genelleştirebiliriz":

```cpp
template<class T>
```

Bu, sınıf tanımına da uygulanabilir. Sınıf tanımındaki tüm `T` örnekleri, tür parametresi ile değiştirilir. Tıpkı fonksiyon şablonlarında olduğu gibi!

Şablon tanımlandıktan sonra, sınıfın nesnelerini bildirebiliriz.

Örneğin, bir `Box` sınıfını şablon olarak tanımlayalım:

```cpp
template<class T>
class Box {
private:
    T value;
public:
    Box(T val) : value(val) {}
    T getValue() const { return value; }
    void setValue(T val) { value = val; }
};
```

Bu şablon sınıfı, `T` türünde bir `value` üyesine sahiptir ve `T` türünde değerler alıp döndüren üye fonksiyonlara sahiptir.

Şimdi, bu şablon sınıfını kullanarak nesneler oluşturabiliriz:

```cpp
int main() {
    Box<int> intBox(123);
    Box<double> doubleBox(456.78);
    Box<std::string> stringBox("Hello");

    std::cout << intBox.getValue() << std::endl;
    std::cout << doubleBox.getValue() << std::endl;
    std::cout << stringBox.getValue() << std::endl;

    return 0;
}
```

Bu şekilde, `Box` sınıfı herhangi bir türdeki değerleri saklayabilir ve işleyebilir. Şablon sınıflar, sınıf tanımlarını genelleştirmenin ve türden bağımsız hale getirmenin güçlü bir yoludur.

Başka bir örnekle:
İşte `Pair` sınıfının şablon tanımı:

```cpp
template<class T>
class Pair
{
public:
    Pair();
    Pair(T firstVal, T secondVal);
    void setFirst(T newVal);
    void setSecond(T newVal);
    T getFirst() const;
    T getSecond() const;
private:
    T first;
    T second;
};
```

Bu şablon sınıfı, iki `T` türünde değeri saklar ve bu değerleri ayarlamak ve almak için üye fonksiyonlara sahiptir. Şimdi, bu sınıfın üye fonksiyonlarının tanımlarını ekleyelim:

```cpp
template<class T>
Pair<T>::Pair() : first(T()), second(T()) {}

template<class T>
Pair<T>::Pair(T firstVal, T secondVal) : first(firstVal), second(secondVal) {}

template<class T>
void Pair<T>::setFirst(T newVal) {
    first = newVal;
}

template<class T>
void Pair<T>::setSecond(T newVal) {
    second = newVal;
}

template<class T>
T Pair<T>::getFirst() const {
    return first;
}

template<class T>
T Pair<T>::getSecond() const {
    return second;
}
```

Bu tanımlarla birlikte, `Pair` sınıfını kullanarak nesneler oluşturabilir ve bu nesnelerle çalışabilirsiniz:

```cpp
int main() {
    Pair<int> intPair(1, 2);
    std::cout << "First: " << intPair.getFirst() << ", Second: " << intPair.getSecond() << std::endl;

    Pair<double> doublePair(3.14, 2.71);
    std::cout << "First: " << doublePair.getFirst() << ", Second: " << doublePair.getSecond() << std::endl;

    Pair<std::string> stringPair("Hello", "World");
    std::cout << "First: " << stringPair.getFirst() << ", Second: " << stringPair.getSecond() << std::endl;

    return 0;
}
```

Bu şekilde, `Pair` sınıfı herhangi bir türdeki iki değeri saklayabilir ve işleyebilir.

## Class Templates as Parameters
Düşünelim:

```cpp
int addUp(const Pair<int>& thePair);
```

Bu fonksiyonda, `Pair<int>` türü `T` olarak sağlanır ve bu sınıf türü parametresi olarak kullanılır. Bu örnekte, çağrı referans ile yapılır. Yine: şablon türleri, standart türlerin kullanılabildiği her yerde kullanılabilir.

Örneğin, `addUp` fonksiyonunu tanımlayalım:

```cpp
int addUp(const Pair<int>& thePair) {
    return thePair.getFirst() + thePair.getSecond();
}
```

Bu fonksiyon, `Pair<int>` türünde bir nesneyi referans olarak alır ve içindeki iki `int` değeri toplar.

Kullanımı:

```cpp
int main() {
    Pair<int> intPair(3, 4);
    std::cout << "Sum: " << addUp(intPair) << std::endl; // Çıktı: Sum: 7

    return 0;
}
```

Bu şekilde, şablon türleri standart türlerin kullanılabildiği her yerde kullanılabilir ve aynı şekilde işlev görebilir.

## Class Templates Within Function Templates

Yeni bir aşırı yükleme tanımlamak yerine, şablon kullanarak genel bir `addUp` fonksiyonu tanımlayabiliriz:
```cpp


template

<class T>
T addUp(const Pair<T>& thePair) {
    // Önkoşul: + operatörü T türündeki değerler için tanımlıdır
    // thePair içindeki iki değerin toplamını döndürür
    return thePair.getFirst() + thePair.getSecond();
}
```

Bu fonksiyon artık her türlü sayı türüne uygulanabilir. Örneğin, `int`, `double`, `float` gibi türler için kullanılabilir.

Kullanımı:

```cpp
int main() {
    Pair<int> intPair(3, 4);
    std::cout << "Sum: " << addUp(intPair) << std::endl; // Çıktı: Sum: 7

    Pair<double> doublePair(3.14, 2.71);
    std::cout << "Sum: " << addUp(doublePair) << std::endl; // Çıktı: Sum: 5.85

    Pair<float> floatPair(1.1f, 2.2f);
    std::cout << "Sum: " << addUp(floatPair) << std::endl; // Çıktı: Sum: 3.3

    return 0;
}
```

Bu şekilde, `addUp` fonksiyonu herhangi bir türdeki `Pair` nesnesi için çalışabilir ve içindeki iki değeri toplayabilir. Şablon fonksiyonları, kodunuzu daha genel ve esnek hale getirir.

## Restrictions on Type Parameter

Sadece "makul" türler `T` için kullanılabilir. Dikkate alınması gerekenler:
- Atama operatörü "düzgün" çalışmalıdır.
- Kopya yapıcı da çalışmalıdır.
- Eğer `T` işaretçiler içeriyorsa, yıkıcı uygun olmalıdır.

Fonksiyon şablonlarında olduğu gibi benzer sorunlar ortaya çıkar.

Örneğin, `Pair` sınıfı için:

```cpp
template<class T>
class Pair
{
public:
    Pair();
    Pair(T firstVal, T secondVal);
    void setFirst(T newVal);
    void setSecond(T newVal);
    T getFirst() const;
    T getSecond() const;
private:
    T first;
    T second;
};
```

Bu sınıfın düzgün çalışması için `T` türünün atama operatörü, kopya yapıcı ve yıkıcı düzgün çalışmalıdır. Örneğin, `int`, `double`, `std::string` gibi türler bu gereksinimleri karşılar.

Ancak, işaretçiler içeriyorsa, yıkıcı uygun olmalıdır. Örneğin:

```cpp
template<class T>
class Pair
{
public:
    Pair();
    Pair(T firstVal, T secondVal);
    ~Pair(); // Yıkıcı
    void setFirst(T newVal);
    void setSecond(T newVal);
    T getFirst() const;
    T getSecond() const;
private:
    T first;
    T second;
};

template<class T>
Pair<T>::~Pair() {
    // Eğer T işaretçi ise, belleği serbest bırakmak gerekebilir
    // delete first; // Eğer first işaretçi ise
    // delete second; // Eğer second işaretçi ise
}
```

Bu şekilde, `Pair` sınıfı işaretçiler içeriyorsa, yıkıcı uygun şekilde tanımlanmalıdır. Şablon sınıflar ve fonksiyonlar, türlerin belirli gereksinimleri karşılamasını gerektirir. Bu nedenle, sadece "makul" türler `T` için kullanılabilir.

## Type Definitions
Özel bir sınıf şablon adını temsil etmek için yeni bir "sınıf türü adı" tanımlayabilirsiniz. Örneğin:

```cpp
// Pair sınıf şablonunun tanımı
template<class T>
class Pair
{
public:
    Pair();
    Pair(T firstVal, T secondVal);
    void setFirst(T newVal);
    void setSecond(T newVal);
    T getFirst() const;
    T getSecond() const;
private:
    T first;
    T second;
};

// Yeni bir sınıf türü adı tanımlama
typedef Pair<int> PairOfInt;

// PairOfInt adı artık Pair<int> türündeki nesneleri bildirmek için kullanılabilir
PairOfInt pair1, pair2;

// PairOfInt adı parametre olarak veya tür adının izin verildiği herhangi bir yerde kullanılabilir
void printPair(const PairOfInt& p) {
    std::cout << "First: " << p.getFirst() << ", Second: " << p.getSecond() << std::endl;
}

int main() {
    pair1.setFirst(1);
    pair1.setSecond(2);
    printPair(pair1);

    return 0;
}
```

Bu şekilde, `Pair<int>` türünü temsil eden `PairOfInt` adını kullanarak nesneler bildirebilir ve bu adı parametre olarak veya tür adının izin verildiği herhangi bir yerde kullanabilirsiniz.

## Friends and Templates

Arkadaş fonksiyonlar, şablon sınıflarla birlikte kullanılabilir. Bu, sıradan sınıflarla olduğu gibi çalışır. Sadece uygun yerlerde tür parametresi gerektirir. Şablon sınıfların arkadaşları olması çok yaygındır, özellikle operatör aşırı yüklemeleri için.

Örneğin, `Pair` sınıfı için `operator<<` aşırı yüklemesini arkadaş fonksiyon olarak tanımlayalım:

```cpp
#include <iostream>

// Pair sınıf şablonunun tanımı
template<class T>
class Pair
{
public:
    Pair() : first(T()), second(T()) {}
    Pair(T firstVal, T secondVal) : first(firstVal), second(secondVal) {}

    void setFirst(T newVal) { first = newVal; }
    void setSecond(T newVal) { second = newVal; }
    T getFirst() const { return first; }
    T getSecond() const { return second; }

    // Arkadaş fonksiyon olarak operator<< aşırı yüklemesi
    template<class U>
    friend std::ostream& operator<<(std::ostream& os, const Pair<U>& pair);

private:
    T first;
    T second;
};

// operator<< aşırı yüklemesinin tanımı
template<class T>
std::ostream& operator<<(std::ostream& os, const Pair<T>& pair)
{
    os << "First: " << pair.first << ", Second: " << pair.second;
    return os;
}

int main() {
    Pair<int> intPair(1, 2);
    std::cout << intPair << std::endl;

    Pair<double> doublePair(3.14, 2.71);
    std::cout << doublePair << std::endl;

    return 0;
}
```

Bu örnekte, `Pair` sınıfı için `operator<<` aşırı yüklemesi arkadaş fonksiyon olarak tanımlanmıştır. Bu sayede, `Pair` sınıfının özel üyelerine erişebilir ve `Pair` nesnelerini `std::cout` ile yazdırabilirsiniz. Şablon sınıflar için arkadaş fonksiyonlar, özellikle operatör aşırı yüklemeleri için çok yaygındır.

## Predefined Template Classes
Evet, `vector` sınıfı bir şablon sınıftır. Bir diğer örnek ise `basic_string` şablon sınıfıdır. Bu sınıf, "herhangi bir türdeki" elemanlardan oluşan dizelerle ilgilenir.

Örneğin:

- `basic_string<char>`: `char` türündeki elemanlarla çalışır.
- `basic_string<double>`: `double` türündeki elemanlarla çalışır.
- `basic_string<YourClass>`: `YourClass` türündeki nesnelerle çalışır.

`std::string` aslında `basic_string<char>`'ın bir tür tanımıdır. İşte bazı örnekler:

```cpp
#include <iostream>
#include <string>
#include <vector>

int main() {
    // std::string, basic_string<char>'ın bir tür tanımıdır
    std::string str = "Hello, World!";
    std::cout << str << std::endl;

    // basic_string<double> kullanımı
    std::basic_string<double> doubleString;
    doubleString.push_back(1.1);
    doubleString.push_back(2.2);
    doubleString.push_back(3.3);
    for (double d : doubleString) {
        std::cout << d << " ";
    }
    std::cout << std::endl;

    // basic_string<YourClass> kullanımı
    class YourClass {
    public:
        YourClass(int val) : value(val) {}
        int getValue() const { return value; }
    private:
        int value;
    };

    std::basic_string<YourClass> yourClassString;
    yourClassString.push_back(YourClass(1));
    yourClassString.push_back(YourClass(2));
    yourClassString.push_back(YourClass(3));
    for (const YourClass& obj : yourClassString) {
        std::cout << obj.getValue() << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

Bu örneklerde, `basic_string` şablon sınıfı farklı türlerdeki elemanlarla çalışmak için kullanılmıştır. `std::string` `char` türündeki elemanlarla çalışırken, `basic_string<double>` `double` türündeki elemanlarla ve `basic_string<YourClass>` `YourClass` türündeki elemanlarla çalışır. Şablon sınıflar, kodunuzu daha esnek ve yeniden kullanılabilir hale getirir.
# Templates and Inheritence

Türetilmiş şablon sınıflar, şablon veya şablon olmayan sınıflardan türetilebilir. Türetilmiş sınıf doğal olarak bir şablon sınıfı olur. Sözdizimi, sıradan bir sınıfın sıradan bir sınıftan türetilmesiyle aynıdır.

Örneğin, bir şablon sınıfından türetilmiş bir şablon sınıfı:

```cpp
#include <iostream>

// Temel şablon sınıfı
template<class T>
class Base {
public:
    Base(T val) : value(val) {}
    T getValue() const { return value; }
protected:
    T value;
};

// Türetilmiş şablon sınıfı
template<class T>
class Derived : public Base<T> {
public:
    Derived(T val) : Base<T>(val) {}
    void showValue() const {
        std::cout << "Value: " << this->value << std::endl;
    }
};

int main() {
    Derived<int> intDerived(42);
    intDerived.showValue(); // Çıktı: Value: 42

    Derived<double> doubleDerived(3.14);
    doubleDerived.showValue(); // Çıktı: Value: 3.14

    return 0;
}
```

Bu örnekte, `Base` adlı bir temel şablon sınıfı ve `Derived` adlı bir türetilmiş şablon sınıfı tanımlanmıştır. `Derived` sınıfı, `Base` sınıfından türetilmiştir ve `Base` sınıfının `value` üyesine erişebilir.

Ayrıca, şablon olmayan bir sınıftan türetilmiş bir şablon sınıfı da tanımlayabilirsiniz:

```cpp
#include <iostream>

// Temel şablon olmayan sınıf
class NonTemplateBase {
public:
    NonTemplateBase(int val) : value(val) {}
    int getValue() const { return value; }
protected:
    int value;
};

// Türetilmiş şablon sınıfı
template<class T>
class DerivedFromNonTemplate : public NonTemplateBase {
public:
    DerivedFromNonTemplate(int val, T extraVal) : NonTemplateBase(val), extraValue(extraVal) {}
    void showValues() const {
        std::cout << "Base Value: " << value << ", Extra Value: " << extraValue << std::endl;
    }
private:
    T extraValue;
};

int main() {
    DerivedFromNonTemplate<double> derived(42, 3.14);
    derived.showValues(); // Çıktı: Base Value: 42, Extra Value: 3.14

    return 0;
}
```

Bu örnekte, `NonTemplateBase` adlı bir şablon olmayan temel sınıf ve `DerivedFromNonTemplate` adlı bir türetilmiş şablon sınıfı tanımlanmıştır. `DerivedFromNonTemplate` sınıfı, `NonTemplateBase` sınıfından türetilmiştir ve `NonTemplateBase` sınıfının `value` üyesine erişebilir.

Bu şekilde, şablon sınıflar ve şablon olmayan sınıflardan türetilmiş şablon sınıflar tanımlayabilirsiniz. Sözdizimi, sıradan sınıfların türetilmesiyle aynıdır.
# Örnek Quiz Sorusu: Genel Veri Depolama Sistemi

#### Soru:
Bir genel veri depolama sistemi oluşturmanız isteniyor. Bu sistemde, farklı türlerdeki verileri saklayabilen bir `Storage` şablon sınıfı ve bu sınıftan türetilen `IntStorage` ve `StringStorage` sınıfları bulunmaktadır. Ayrıca, `Storage` sınıfı, verileri eklemek (`add`), almak (`get`) ve listelemek (`list`) için işlevler sağlar.

Aşağıdaki UML diyagramını kullanarak sınıfları oluşturun ve belirtilen işlevleri gerçekleştirin:

#### UML Diyagramı:

```
					+-------------------+
					|     Storage<T>    |
					+-------------------+
					| - data: vector<T> |
					+-------------------+
					| + add(item: T):   |
					|   void            |
					| + get(index: int):|
					|   T               |
					| + list(): void    |
					+-------------------+
					          /\
					         /  \
					        /    \
		+-------------------+    +-------------------+
		|    IntStorage     |    |   StringStorage   |
		+-------------------+    +-------------------+
		| + IntStorage()    |    | + StringStorage() |
		+-------------------+    +-------------------+
```

#### Yapılacaklar:
1. Yukarıdaki UML diyagramına göre `Storage` şablon sınıfını ve `IntStorage` ile `StringStorage` sınıflarını oluşturun.
2. `Storage` sınıfında `add`, `get` ve `list` işlevlerini tanımlayın.
3. `main` fonksiyonunda `IntStorage` ve `StringStorage` nesneleri oluşturun, veriler ekleyin ve listeleyin.

#### Kod (Cevap):
```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Storage şablon sınıfı
template <class T>
class Storage {
protected:
    vector<T> data;
public:
    void add(T item) {
        data.push_back(item);
    }

    T get(int index) {
        if (index >= 0 && index < data.size()) {
            return data[index];
        } else {
            throw out_of_range("Index out of range");
        }
    }

    void list() const {
        for (const auto& item : data) {
            cout << item << " ";
        }
        cout << endl;
    }
};

// IntStorage sınıfı
class IntStorage : public Storage<int> {
public:
    IntStorage() = default;
};

// StringStorage sınıfı
class StringStorage : public Storage<string> {
public:
    StringStorage() = default;
};

int main() {
    // IntStorage nesnesi oluşturma ve veri ekleme
    IntStorage intStorage;
    intStorage.add(1);
    intStorage.add(2);
    intStorage.add(3);
    cout << "IntStorage list: ";
    intStorage.list();

    // StringStorage nesnesi oluşturma ve veri ekleme
    StringStorage stringStorage;
    stringStorage.add("Hello");
    stringStorage.add("World");
    cout << "StringStorage list: ";
    stringStorage.list();

    // Verileri alma
    try {
        cout << "First element in IntStorage: " << intStorage.get(0) << endl;
        cout << "First element in StringStorage: " << stringStorage.get(0) << endl;
    } catch (const out_of_range& e) {
        cerr << e.what() << endl;
    }

    return 0;
}
```

Bu kodu yazın ve çalıştırın. Çıktıda, `IntStorage` ve `StringStorage` nesnelerinin verileri listelediğini ve belirli indekslerdeki verileri aldığını göreceksiniz. Bu, şablon sınıflar, türetilmiş sınıflar ve genel veri depolama kavramlarını anlamanıza yardımcı olacaktır.