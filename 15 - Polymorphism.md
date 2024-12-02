*Links*: [[00 - Index]]
*Date*: 26.11.2024
*Resources*: [name]()

---
# Virtual Functions
Polymorphism (çok biçimlilik), nesne yönelimli programlamada bir işlemin farklı nesne türleri tarafından farklı şekillerde gerçekleştirilmesini sağlayan bir kavramdır. C++'da polymorphism, genellikle sanal fonksiyonların kullanımıyla sağlanır ve iki ana türü vardır:

- Derleme Zamanı Polymorphism: Fonksiyon aşırı yükleme ve operatör aşırı yükleme ile gerçekleştirilir.
- Çalışma Zamanı Polymorphism: Sanal fonksiyonlar ve sınıf hiyerarşisi ile gerçekleştirilir.

Bu sayede, aynı arayüze sahip farklı nesneler farklı davranışlar sergileyebilir.

C++'da çok biçimlilik (polymorphism), bir fonksiyona birden fazla anlamın ilişkilendirilmesini sağlayan bir kavramdır. Bu, nesne yönelimli programlamanın temel prensiplerinden biridir. Çok biçimlilik, sanal fonksiyonlar (virtual functions) aracılığıyla sağlanır. Sanal fonksiyonlar, bir fonksiyonun farklı sınıflarda farklı şekillerde uygulanmasını sağlar.

### 1. **Sanal Fonksiyonlar (Virtual Functions):**
   - **Tanım:** Sanal fonksiyonlar, temel sınıfta tanımlanan ve türetilmiş sınıflarda yeniden tanımlanabilen fonksiyonlardır. Bu, çok biçimliliği sağlar ve temel sınıfın işaretçisi veya referansı aracılığıyla türetilmiş sınıfın fonksiyonunu çağırmanıza olanak tanır.
   - **Örnek Kod:**
     ```cpp
     #include <iostream>

     // Temel Sınıf
     class Base {
     public:
         virtual void display() {
             std::cout << "Base class display" << std::endl;
         }
     };

     // Türetilmiş Sınıf
     class Derived : public Base {
     public:
         void display() override {
             std::cout << "Derived class display" << std::endl;
         }
     };

     int main() {
         Base* basePtr = new Derived();
         basePtr->display();  // Çıktı: Derived class display
         delete basePtr;
         return 0;
     }
     ```

### 2. **Çok Biçimlilik (Polymorphism):**
   - **Tanım:** Çok biçimlilik, bir fonksiyona birden fazla anlamın ilişkilendirilmesini sağlar. Bu, farklı sınıfların aynı adlı fonksiyonları farklı şekillerde uygulamasını sağlar.
   - **Örnek Kod:**
     ```cpp
     #include <iostream>

     // Temel Sınıf
     class Shape {
     public:
         virtual void draw() {
             std::cout << "Drawing a shape" << std::endl;
         }
     };

     // Türetilmiş Sınıf 1
     class Circle : public Shape {
     public:
         void draw() override {
             std::cout << "Drawing a circle" << std::endl;
         }
     };

     // Türetilmiş Sınıf 2
     class Square : public Shape {
     public:
         void draw() override {
             std::cout << "Drawing a square" << std::endl;
         }
     };

     int main() {
         Shape* shapes[2];
         shapes[0] = new Circle();
         shapes[1] = new Square();

         for (int i = 0; i < 2; i++) {
             shapes[i]->draw();
         }

         delete shapes[0];
         delete shapes[1];
         return 0;
     }
     ```
   - **Çıktı:**
     ```
     Drawing a circle
     Drawing a square
     ```

### 3. **Sanal Fonksiyonların Avantajları:**
   - **Esneklik:** Sanal fonksiyonlar, farklı sınıfların aynı adlı fonksiyonları farklı şekillerde uygulamasını sağlar. Bu, kodun daha esnek ve genişletilebilir olmasını sağlar.
   - **Çok Biçimlilik:** Sanal fonksiyonlar, çok biçimliliği sağlar ve temel sınıfın işaretçisi veya referansı aracılığıyla türetilmiş sınıfın fonksiyonunu çağırmanıza olanak tanır.

### 4. **Sanal Fonksiyonların Tanımı:**
   - **Sanal (Virtual):** "Sanal" kelimesi, bir şeyin "varlığının özünde" olduğu, ancak gerçekte olmadığı anlamına gelir. Sanal fonksiyonlar, temel sınıfta tanımlanır ve türetilmiş sınıflarda yeniden tanımlanabilir.
   - **Sanal Fonksiyon (Virtual Function):** Bir fonksiyonun, tanımlandığı sırada kullanılabilmesini sağlar. Bu, çok biçimliliği sağlar ve farklı sınıfların aynı adlı fonksiyonları farklı şekillerde uygulamasını sağlar.
# **Virtual Fonksiyonlar ve Türetilmiş Sınıflar**

1. **Otomatik Sanallaştırma**: Bir temel sınıfta (base class) bir fonksiyon `virtual` olarak tanımlandığında, türetilen sınıflarda (derived class) bu fonksiyon **otomatik olarak sanal** olur. Türetilen sınıfta, bu fonksiyonun üzerine yazıldığında (override), `virtual` anahtar kelimesi kullanılmasa bile sanal olarak çalışmaya devam eder.
    
2. **`virtual` Anahtar Kelimesi Gerekli mi?**  
    Türetilen sınıfta, sanal olduğunu belirtmek için `virtual` anahtar kelimesini kullanmak **gerekli değildir**. Ancak **okunabilirlik ve kodun anlaşılabilirliğini artırmak** için genellikle kullanılır.
    

### **Örnek:**

#### Temel Sınıfta Sanal Fonksiyon

```cpp
class Base {
public:
    virtual void show() const {
        std::cout << "Base class show function\n";
    }
};
```

#### Türetilmiş Sınıfta `virtual` Kullanımı

```cpp
class Derived : public Base {
public:
    // 'virtual' yazılmasa bile 'show' sanaldır.
    void show() const override { 
        std::cout << "Derived class show function\n";
    }
};
```

### **Kapsamlı Örnek:**

```cpp
class Base {
public:
    virtual void display() const {
        std::cout << "Base class display\n";
    }
};

class Derived1 : public Base {
public:
    // 'virtual' eklenmemiş ama yine de sanaldır.
    void display() const override {
        std::cout << "Derived1 class display\n";
    }
};

class Derived2 : public Base {
public:
    virtual void display() const override { // 'virtual' isteğe bağlı olarak eklenmiş
        std::cout << "Derived2 class display\n";
    }
};

int main() {
    Base* basePtr;

    Derived1 d1;
    Derived2 d2;

    basePtr = &d1;
    basePtr->display(); // Derived1 class display

    basePtr = &d2;
    basePtr->display(); // Derived2 class display

    return 0;
}
```

### **Kodun Çalışma Mantığı:**

1. `display` fonksiyonu temel sınıfta `virtual` olarak tanımlandığı için türetilen sınıflarda otomatik olarak sanaldır.
2. Türetilen sınıfta `virtual` yazılmasa bile polimorfizm çalışır.
3. `override` anahtar kelimesi, türetilen sınıfta bir sanal fonksiyonun temel sınıftaki sanal fonksiyonu gerçekten geçersiz kıldığını (override ettiğini) açıkça belirtir.

### **Kod Stili Önerisi:**

- **`virtual` Kullanımı:** Türetilen sınıfta `virtual` yazmak zorunlu olmasa da, kodun daha okunaklı olmasını sağlar. Bu nedenle **kodda açıklık ve tutarlılık** sağlamak için kullanılması önerilir.
- **`override` Kullanımı:** Fonksiyonun temel sınıftaki bir sanal fonksiyonu geçersiz kıldığını açıkça belirtmek için `override` anahtar kelimesi kullanılması önemlidir. Bu, olası hataları önler.

Sonuç olarak, `virtual` yazmak türetilmiş sınıflarda bir gereklilik olmasa da, **iyi bir yazılım geliştirme pratiği olarak kullanılır.**

# **Late Binding (Geç Bağlama) Nedir?**

Geç bağlama, programın çalışması sırasında hangi fonksiyonun çağrılacağına karar verilmesidir. Bu, çalışma zamanı bilgisine dayanır ve polimorfizm ile doğrudan ilişkilidir.

- **Erken Bağlama (Early Binding):** Derleme zamanında hangi fonksiyonun çağrılacağına karar verilir.
- **Geç Bağlama (Late Binding):** Çağrılacak fonksiyon, nesnenin türüne bağlı olarak çalışma zamanında belirlenir.

### **Virtual Functions ile Late Binding**

C++'ta **virtual** fonksiyonlar, geç bağlamayı uygulamak için kullanılır. Bir fonksiyon sanal olarak tanımlandığında, çağrılacak olan fonksiyonun sürümü çalışma zamanında belirlenir. Bu süreç, çağrının yapıldığı nesne türüne göre gerçekleşir.

### **Nasıl Çalışır?**

1. **Temel Sınıfta Virtual Fonksiyon:** Bir temel sınıfta (base class) sanal bir fonksiyon tanımlandığında, türetilmiş sınıflar (derived classes) bu fonksiyonu geçersiz kılabilir (override).
2. **Geç Bağlama:** Bir temel sınıf işaretçisi veya referansı, türetilmiş sınıfın nesnesine işaret ediyorsa, çağrılan fonksiyon türetilmiş sınıfta yeniden tanımlanmışsa, türetilmiş sınıftaki sürüm çağrılır.

### **Kod Örneği**

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    virtual void sound() const { // Virtual function
        cout << "Animal makes a sound" << endl;
    }
    virtual ~Animal() {}
};

class Dog : public Animal {
public:
    void sound() const override { // Overrides the virtual function
        cout << "Dog barks" << endl;
    }
};

class Cat : public Animal {
public:
    void sound() const override { // Overrides the virtual function
        cout << "Cat meows" << endl;
    }
};

int main() {
    Animal* animal1 = new Dog();
    Animal* animal2 = new Cat();

    // Late binding: Decides at runtime which sound() to call
    animal1->sound(); // Output: Dog barks
    animal2->sound(); // Output: Cat meows

    delete animal1;
    delete animal2;

    return 0;
}
```

### **Geç Bağlama'nın Önemi**

- **Polimorfizm:** Geç bağlama, polimorfizmin temel taşıdır ve C++'ta nesne yönelimli programlamanın güçlü bir özelliğidir.
- **Esneklik:** Temel sınıf işaretçileri veya referansları kullanarak türetilmiş sınıflarla çalışabilirsiniz.
- **Modülerlik:** Temel sınıfın yeniden derlenmesine gerek kalmadan türetilmiş sınıflar eklenebilir.

### **Nasıl İşler?**

- Derleyici, temel sınıftaki `virtual` fonksiyonlar için bir **vtable** (sanal fonksiyon tablosu) oluşturur. Her sınıfın kendine özgü bir vtable'ı vardır.
- Bir sanal fonksiyon çağrıldığında, çalışma zamanında vtable'daki doğru girişe başvurularak çağrılacak fonksiyon belirlenir.

### **Sonuç**

Virtual fonksiyonlar, geç bağlama (late binding) mekanizmasını destekleyerek nesne yönelimli programlamada esneklik ve genişletilebilirlik sağlar. Bu, özellikle farklı nesnelerin aynı temel sınıf üzerinden farklı davranışlar sergilemesi gerektiğinde çok güçlü bir araçtır.


# **Virtual Fonksiyonun Türetilmiş Sınıfta Değiştirilmesi**

Bir **virtual** fonksiyon, türetilmiş bir sınıfta yeniden tanımlandığında bu işleme **override (geçersiz kılma)** denir. Bu, türetilmiş sınıfın, temel sınıfın (base class) varsayılan davranışını değiştirmek istediği durumlarda kullanılır.

#### **Özellikleri:**

1. Sanal fonksiyonlar türetilmiş sınıfta **aynı imza (signature)** ile yeniden tanımlanır.
2. Polimorfizm ile desteklenir: Çağrılan fonksiyonun hangi sürümünün kullanılacağı çalışma zamanında (runtime) belirlenir.
3. `override` anahtar kelimesi (C++11 ve sonrası), türetilmiş sınıfta bir fonksiyonun gerçekten temel sınıftaki bir sanal fonksiyonu geçersiz kıldığını açıkça belirtmek için kullanılabilir.

### **Non-Virtual Fonksiyonun Türetilmiş Sınıfta Değiştirilmesi**

Bir **non-virtual** fonksiyon, türetilmiş sınıfta yeniden tanımlandığında buna **redefine (yeniden tanımlama)** denir. Bu işlem polimorfizm ile desteklenmez; fonksiyonun hangi sürümünün çağrılacağı derleme zamanında (compile-time) belirlenir.

#### **Özellikleri:**

1. Türetilmiş sınıfta aynı isimle tanımlanabilir.
2. **Temel sınıf işaretçisi veya referansı** kullanıldığında temel sınıfın fonksiyonu çağrılır.
3. Bu işlem, türetilmiş sınıfın bir fonksiyonun davranışını sadece kendi kullanımında değiştirmesi gerektiği durumlarda kullanılır.

### **Karşılaştırmalı Örnek**

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void virtualFunction() const { // Virtual function
        cout << "Base class virtual function" << endl;
    }
    void nonVirtualFunction() const { // Non-virtual function
        cout << "Base class non-virtual function" << endl;
    }
};

class Derived : public Base {
public:
    void virtualFunction() const override { // Overridden function
        cout << "Derived class virtual function" << endl;
    }
    void nonVirtualFunction() const { // Redefined function
        cout << "Derived class non-virtual function" << endl;
    }
};

int main() {
    Base* basePtr = new Derived();

    // Virtual function: Late binding (runtime decision)
    basePtr->virtualFunction(); // Output: Derived class virtual function

    // Non-virtual function: Early binding (compile-time decision)
    basePtr->nonVirtualFunction(); // Output: Base class non-virtual function

    delete basePtr;
    return 0;
}
```

### **Sonuçlar:**
1. **Sanal Fonksiyonlar:**
    - Türetilmiş sınıfta **override** edilir.
    - Polimorfizm sayesinde türetilmiş sınıftaki sürüm çalıştırılır.
2. **Non-Sanal Fonksiyonlar:**
    - Türetilmiş sınıfta **redefine** edilir.
    - Temel sınıf işaretçileri veya referansları kullanıldığında her zaman temel sınıftaki sürüm çalıştırılır.

### **Önemli Notlar:**
- **override Anahtar Kelimesi:** Kullanılması önerilir çünkü temel sınıfta eşleşen bir fonksiyon yoksa derleyici hata verir.
- **Kapsama (Scope):** Non-virtual fonksiyonların türetilmiş sınıfta yeniden tanımlanması, türetilmiş sınıfın kapsama alanı içinde geçerlidir; temel sınıf referansları bundan etkilenmez.

Bu ayrım, sanal fonksiyonların esnekliğini ve polimorfizmin gücünü anlamak için çok önemlidir.

# **Virtual Fonksiyonların Avantajları**

1. **Polimorfizm Sağlar:** Virtual fonksiyonlar, çalışma zamanında doğru fonksiyonun çağrılmasını sağlar. Bu, farklı sınıfların bir temel sınıf üzerinden benzer bir arayüzle kullanılabilmesini mümkün kılar.
2. **Esneklik ve Genişletilebilirlik:** Programlara esneklik katar, çünkü türetilmiş sınıflar, temel sınıftaki davranışı kendi ihtiyaçlarına göre geçersiz kılabilir.
3. **Geç Bağlama (Late Binding):** Hangi fonksiyonun çağrılacağı, çağrının yapıldığı nesneye bağlı olarak çalışma zamanında belirlenir.

# **Virtual Fonksiyonların Dezavantajları**

1. **Bellek Kullanımı (Storage Overhead):**
    
    - Virtual fonksiyonlar, **vtable (sanal fonksiyon tablosu)** ve işaretçileri kullanır. Her sınıf için bir vtable ve her nesne için bir işaretçi saklanması gerekir. Bu, ek bellek kullanımına yol açar.
2. **Performans Kaybı (Runtime Overhead):**
    
    - Geç bağlama işlemi çalışma zamanında gerçekleştiği için, sanal fonksiyon çağrıları **normal fonksiyon çağrılarından daha yavaştır.** Sanal olmayan bir fonksiyonun çağrısı derleme zamanında çözülürken, sanal bir fonksiyon için vtable üzerinden doğru fonksiyon bulunur.
3. **Basit Durumlarda Gereksiz Kullanım:**
    
    - Eğer polimorfizm veya geç bağlama gerekli değilse, virtual fonksiyonlar gereksiz yere kullanıldığında performans kaybına ve kaynak israfına neden olur.

### **Kullanılmalı mı, Kullanılmamalı mı?**

1. **Kullanılmalı:**
    
    - Farklı türetilmiş sınıfların farklı davranışlar sergilemesi gerektiğinde.
    - Polimorfizm ve esneklik ihtiyacı olduğunda.
    - Temel sınıf üzerinden türetilmiş sınıflara erişim sağlanması gereken durumlarda.
2. **Kullanılmamalı:**
    
    - Polimorfizm gerekmiyorsa.
    - Fonksiyonlar temel sınıfta ve türetilmiş sınıflarda aynı şekilde çalışıyorsa.
    - Performans kritik bir faktörse ve düşük gecikme veya daha az bellek kullanımı öncelikliyse.

### **Örnek: Performans Kıyaslaması**

#### Virtual Fonksiyon (Geç Bağlama)

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void doSomething() const {
        cout << "Base class function" << endl;
    }
};

class Derived : public Base {
public:
    void doSomething() const override {
        cout << "Derived class function" << endl;
    }
};

void callFunction(const Base& obj) {
    obj.doSomething();
}

int main() {
    Derived d;
    callFunction(d); // Late binding (vtable lookup)
    return 0;
}
```

#### Non-Virtual Fonksiyon (Erken Bağlama)

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    void doSomething() const {
        cout << "Base class function" << endl;
    }
};

class Derived : public Base {
public:
    void doSomething() const {
        cout << "Derived class function" << endl;
    }
};

void callFunction(const Base& obj) {
    obj.doSomething(); // Early binding
}

int main() {
    Derived d;
    callFunction(d); // Calls Base class function due to early binding
    return 0;
}
```

### **Sonuç**

- **Avantajları:** Virtual fonksiyonlar, polimorfizmin uygulanması için temel taşlardan biridir. Esneklik ve genişletilebilirlik sağlar.
- **Dezavantajları:** Geç bağlama nedeniyle performans kaybına ve bellek kullanımında artışa neden olabilir.
- **En İyi Pratik:** Eğer bir fonksiyonun türetilmiş sınıflarda farklı davranış sergilemesi gerekmiyorsa veya performans kritikse, virtual fonksiyonlar kullanılmamalıdır. Kod tasarımında **gereksiz karmaşıklıktan kaçınmak için** doğru durumu değerlendirmek önemlidir.

# Saf Sanal Fonksiyon Nedir?

`virtual` fonksiyonun yanındaki `= 0`, bu fonksiyonun **pure virtual** (saf sanal) bir fonksiyon olduğunu belirtir.

Saf sanal fonksiyonlar, bir sınıfta tanımlanan ancak gövdesi olmayan fonksiyonlardır. Bu tür fonksiyonlar, türetilen sınıflarda **mutlaka** yeniden tanımlanmalıdır. Bir sınıfta bir veya daha fazla saf sanal fonksiyon varsa, o sınıf **soyut sınıf (abstract class)** olarak adlandırılır ve bu sınıftan doğrudan nesne oluşturulamaz.

### Kullanım Amacı

Saf sanal fonksiyonlar, bir temel sınıfın (base class) türetilmiş sınıflar için bir **arayüz (interface)** sağlamasına olanak tanır. Temel sınıf, yalnızca genel bir yapıyı belirler ve detayları türetilmiş sınıflara bırakır.

### Örnek

```cpp
class Shape {
public:
    virtual void draw() const = 0; // Pure virtual function
    virtual ~Shape() {} // Virtual destructor
};

class Circle : public Shape {
public:
    void draw() const override {
        std::cout << "Drawing a circle" << std::endl;
    }
};

class Square : public Shape {
public:
    void draw() const override {
        std::cout << "Drawing a square" << std::endl;
    }
};

int main() {
    Shape* shapes[] = {new Circle(), new Square()};
    
    for (const auto& shape : shapes) {
        shape->draw(); // Calls the appropriate derived class implementation
    }

    for (const auto& shape : shapes) {
        delete shape; // Clean up memory
    }

    return 0;
}
```

### Detaylı Açıklama

1. **Soyut Sınıf (Abstract Class):** `Shape` sınıfı bir soyut sınıftır çünkü içinde saf sanal fonksiyon (`draw`) bulunmaktadır. Bu sınıftan doğrudan nesne oluşturulamaz:
    
    ```cpp
    Shape s; // HATA! Soyut sınıflardan nesne oluşturulamaz.
    ```
    
2. **Türemiş Sınıflar:** `Circle` ve `Square`, `Shape` sınıfını türetmiş ve `draw()` fonksiyonunu yeniden tanımlamıştır. Eğer türetilen bir sınıf bu saf sanal fonksiyonu tanımlamazsa, o sınıf da soyut sınıf olur.
    
3. **Polimorfizm (Çok Biçimlilik):** `Shape*` türünde bir işaretçi kullanılarak, doğru türetilmiş sınıfın `draw()` fonksiyonu çağrılır. Bu, sanallaştırmanın sağladığı esnekliktir.
    
### Neden `= 0` Kullanılır?

- `= 0` yazımı, fonksiyonun gövdesiz olduğunu açıkça belirtir.
- Derleyiciye, bu fonksiyonun türetilen sınıfta tanımlanması gerektiğini söyler.
- Arayüz tasarımında önemli bir rol oynar, çünkü türetilen sınıfların belirli bir davranışı sağlamasını zorunlu kılar.

Bu yaklaşım, programlama prensiplerinden **Open/Closed Principle** (Açık/Kapalı Prensibi) ve **Liskov Substitution Principle** ile uyumlu bir yapı oluşturur.

# **Soyut Sınıf (Abstract Class) ve Amaçları**

1. **Soyut Sınıf Nedir?**
    
    - C++’ta bir veya daha fazla **pure virtual function** içeren bir sınıfa **soyut sınıf** denir.
    - Bir soyut sınıfın **doğrudan bir nesnesi oluşturulamaz**. Bu sınıf yalnızca başka sınıflar için bir temel oluşturur.
2. **Kullanım Durumu:**
    
    - Temel sınıfın kendisi bir işlevi tam anlamıyla gerçekleştiremiyorsa (örneğin, `Figure` sınıfının bir şekli çizememesi gibi), türetilmiş sınıflar için bir çerçeve sağlar.
    - Tüm türetilmiş sınıflar, soyut sınıfta tanımlanmış olan pure virtual function’ları **uygulamak zorundadır.**

### **Pure Virtual Function Nedir?**

1. **Tanımı:**
    
    - Bir virtual fonksiyonun "pure" (saf) olabilmesi için **`= 0`** ifadesiyle tanımlanması gerekir.
    - Bu, fonksiyonun **temel sınıfta bir tanımı olmadığını** ve türetilmiş sınıfların bu fonksiyonu geçersiz kılmak (override) zorunda olduğunu belirtir.
2. **Sözdizimi:**
    
    ```cpp
    class Base {
    public:
        virtual void pureVirtualFunction() = 0; // Pure virtual function
    };
    ```
    

### **Örnek: Soyut Sınıf ve Pure Virtual Function**

```cpp
#include <iostream>
using namespace std;

// Abstract class
class Figure {
public:
    virtual void draw() const = 0; // Pure virtual function
    virtual ~Figure() {}
};

// Derived classes
class Rectangle : public Figure {
public:
    void draw() const override {
        cout << "Drawing a rectangle" << endl;
    }
};

class Circle : public Figure {
public:
    void draw() const override {
        cout << "Drawing a circle" << endl;
    }
};

int main() {
    // Figure f; // Error! Cannot instantiate an abstract class.

    Rectangle rect;
    Circle circ;

    Figure* figures[] = { &rect, &circ };

    for (Figure* fig : figures) {
        fig->draw(); // Calls the correct draw() method via polymorphism
    }

    return 0;
}
```

### **Kod Çalışma Mantığı**

1. **`Figure` Sınıfı:**
    
    - Bu sınıf bir soyut sınıftır. Çünkü `draw()` bir **pure virtual function** olarak tanımlanmıştır.
    - `Figure` sınıfı yalnızca bir çerçeve sunar; bir nesne olarak kullanılamaz.
2. **Türetilmiş Sınıflar (`Rectangle` ve `Circle`):**
    
    - `Rectangle` ve `Circle`, `Figure` sınıfını türetir ve `draw()` fonksiyonunu uygular.
    - Türetilmiş sınıflar, `Figure` arayüzüyle uyumlu olmak zorundadır.
3. **Polimorfizm ve Pure Virtual Function:**
    
    - `Figure*` işaretçisi üzerinden türetilmiş sınıfların `draw()` fonksiyonları çağrılır.
    - Geç bağlama (late binding) mekanizması sayesinde doğru `draw()` sürümü çalıştırılır.

### **Pure Virtual Function’ların Avantajları**

1. **Zorunluluk Sağlar:** Türetilmiş sınıfların, temel sınıfta tanımlanan pure virtual fonksiyonları uygulamasını zorunlu kılar.
2. **Soyutlama:** Temel sınıf, ortak özellikleri ve işlevleri tanımlar; spesifik davranışları türetilmiş sınıflara bırakır.
3. **Polimorfizm ile Uyumluluk:** Soyut sınıflar, polimorfizm için bir arayüz sağlar.

### **Ne Zaman Kullanılmalı?**

- Temel sınıfın, türetilmiş sınıfların uygulaması gereken bir arayüz sağlaması gerekiyorsa.
- Temel sınıfta bir fonksiyonun varsayılan bir tanımına gerek yoksa (örneğin, `Figure` sınıfı çizim detaylarını bilemez).

Bu yöntem, **nesne yönelimli programlamada** soyutlama ve genişletilebilirlik için çok önemli bir araçtır.

# **Kalıtım ve Tür Dönüşümü (Type Conversion)**

1. **Derived Sınıfı, Base Sınıfından Türetilir:**
    
    - `Derived` sınıfı, `Base` sınıfından türetilmiş bir sınıftır. Yani, `Derived` nesneleri, `Base` türündeki değişkenlere atanabilir.
    - Bu, **"is-a"** ilişkisinin temelidir. Bir `Derived` nesnesi, bir `Base` nesnesi olarak kullanılabilir çünkü bir `Derived` sınıfı, temel sınıfının tüm özelliklerine sahip olabilir.
    
    ```cpp
    Base* basePtr;
    Derived derivedObj;
    basePtr = &derivedObj; // Valid: Derived "is a" Base
    ```
    
2. **Ters Yönlü Dönüşüm Mümkün Değil:**
    
    - `Base` sınıfındaki bir nesne, doğrudan bir `Derived` sınıfı türüne dönüştürülemez. Çünkü bir `Base` nesnesi, türetilmiş sınıfın tüm özelliklerine sahip olmayabilir ve bu yüzden tür dönüşümü güvenli değildir.
    - Yani, `Base` bir `Derived`'i **"is-a"** ilişkisini **garanti etmez**.
    
    ```cpp
    Base baseObj;
    Derived* derivedPtr;
    derivedPtr = &baseObj; // Error: Base is not necessarily a Derived
    ```
    

### **"Is-a" İlişkisi**

- **"Is-a" İlişkisi (Inheritance):** Eğer bir sınıf `Base` sınıfından türetilmişse, bu sınıfın nesneleri **"is-a"** ilişkisini kurar. Yani, `Derived` bir `Base`’dir.
    
    - Örneğin, `DiscountSale` sınıfı `Sale` sınıfından türetilmişse, `DiscountSale` nesneleri bir **"Sale"** nesnesidir, ancak her **"Sale"** nesnesi bir `DiscountSale` nesnesi değildir.
    
    ```cpp
    class Sale {
    public:
        virtual void calculate() = 0;
    };
    
    class DiscountSale : public Sale {
    public:
        void calculate() override {
            cout << "Discounted sale calculation" << endl;
        }
    };
    ```
    
    Burada, **`DiscountSale`** bir **`Sale`**'dir, fakat her **`Sale`** nesnesi **`DiscountSale`** değildir.
    

### **Kodla Açıklama**

Aşağıdaki örnekte, `DiscountSale` sınıfı `Sale` sınıfından türetilmiştir. Bir `DiscountSale` nesnesi, `Sale` türünde bir işaretçiye atanabilir, ancak tersine dönüşüm (yani `Sale` nesnesini `DiscountSale` türüne dönüştürmek) mümkün değildir.

```cpp
#include <iostream>
using namespace std;

class Sale {
public:
    virtual void calculate() {
        cout << "Sale calculation" << endl;
    }
};

class DiscountSale : public Sale {
public:
    void calculate() override {
        cout << "Discounted sale calculation" << endl;
    }
};

int main() {
    DiscountSale discount;
    Sale* salePtr = &discount;  // Valid: DiscountSale "is a" Sale
    salePtr->calculate(); // Output: Discounted sale calculation

    // Base class object cannot be assigned to derived class pointer
    Sale saleObj;
    // DiscountSale* discountPtr = &saleObj; // Error: Sale is not necessarily a DiscountSale
}
```

### **Önemli Noktalar:**

- **Türetilmiş Sınıf Nesnesi (`Derived`) Base Türüne Atanabilir:** `DiscountSale` nesnesi bir `Sale` nesnesine atanabilir çünkü **"DiscountSale" bir "Sale"dir**.
- **Base Sınıf Nesnesi (`Base`) Türetilmiş Sınıf Türüne Atanamaz:** `Sale` nesnesi, `DiscountSale` nesnesine dönüştürülemez çünkü bir `Sale`, **"DiscountSale" olabilir** ama her `Sale`, bir `DiscountSale` değildir.

### **Sonuç:**

- **"is-a" ilişkisi**, kalıtımın temelidir. Eğer `Derived` sınıfı `Base` sınıfından türetilmişse, `Derived` nesneleri **"Base" türü** olarak kullanılabilir.
- Ancak **tersine dönüşüm**, yani `Base` nesnesinin `Derived` türüne dönüştürülmesi, mantıklı değildir ve C++’ta bu şekilde bir dönüşüm yapılamaz.

# **Object Slicing (Nesne Dilimleme)**

1. **Tanım:**
    
    - **Object slicing**, türetilmiş bir sınıfın nesnesinin, temel sınıf türündeki bir değişkene atanması sonucu, türetilmiş sınıfın özel özelliklerinin kaybolması durumudur.
    - Bu durumda, **türetilmiş sınıfın** tüm üyeleri **temel sınıfın** üyelerine "dilimlenir" ve **sadece temel sınıfın üyeleri** saklanır.
2. **Örnek Durum:**
    
    - `Dog` sınıfından türetilen bir nesne, bir `Pet` türündeki değişkene atanırsa, `Dog` nesnesinin **`breed`** gibi `Dog`'a özel üyeleri kaybolur. Bu durum **nesne dilimleme** olarak bilinir.
    - `Pet` sınıfının türündeki bir değişken, `Dog` nesnesini doğru şekilde saklayamaz çünkü `Pet` sınıfı `Dog` sınıfından daha az özellik içeriyor.

### **Kod Örneği: Object Slicing**

```cpp
#include <iostream>
using namespace std;

class Pet {
public:
    string name;
    string breed;
};

class Dog : public Pet {
public:
    string owner;
};

int main() {
    Dog vdog;        // Derived class object
    vdog.name = "Buddy";
    vdog.breed = "Golden Retriever";
    vdog.owner = "Alice";

    Pet vpet;        // Base class object
    vpet = vdog;     // Object slicing occurs here

    cout << "vpet name: " << vpet.name << endl;
    cout << "vpet breed: " << vpet.breed << endl;  // ERROR: breed is sliced off
    cout << "vpet owner: " << vpet.owner << endl;  // ERROR: owner does not exist in Pet

    return 0;
}
```

### **Açıklamalar:**

1. **Nesne Dilimleme (Object Slicing) Durumu:**
    
    - `vpet = vdog;` satırında **nesne dilimleme** gerçekleşir. Bu, `Dog` türündeki nesnenin, `Pet` türündeki bir değişkene atanmasıdır.
    - Sonuç olarak, `Dog` sınıfının **`owner`** gibi `Dog`'a özgü üyeleri kaybolur. Sadece **`name`** ve **`breed`** gibi `Pet` sınıfında tanımlı üyeler korunur.
2. **Hata Durumu:**
    
    - `vpet.owner` ve `vpet.breed`'e erişmeye çalıştığınızda hata alırsınız. Çünkü `Pet` sınıfı, `Dog` sınıfının özel üyelerini içermez.
    - `vpet.breed` ve `vpet.owner`'a erişmeye çalıştığınızda, `vpet` sadece `Pet` sınıfını temsil ettiği için, **`owner`** üyesine erişilemez. Ayrıca **`breed`** üyesi de, temel sınıf türüne atanmış bir nesnede kaybolmuş olur.
3. **Neden Hata Alınıyor?**
    
    - `Pet` sınıfı, yalnızca temel sınıfın üyelerini saklar ve `Dog` sınıfının eklediği `owner` gibi üyeler **dilimlenir**.
    - Bu, **türetilmiş sınıfın** üyelerinin kaybolmasına ve **sadece temel sınıfın** üyelerinin kalmasına yol açar.

### **Felsefi Tartışma:**

- **"Dog" Nesnesi Nereye Gitti?**
    
    - Bir `Dog` nesnesi, bir `Pet` türündeki değişkene atandığında, `Dog` nesnesinin özel üyeleri kaybolur ve sadece temel sınıfın üyeleri **görünür hale gelir**. Bu durum, programın nasıl çalıştığını daha doğru bir şekilde anlamanızı sağlar.
    - Türetilmiş sınıfın tüm özellikleri kaybolur, çünkü temel sınıf, türetilmiş sınıfın tüm özelliklerini "bilmez" ve yalnızca kendi tanımlı özelliklerine sahiptir.
- **Felsefi Bir Bakış Açısı:**
    
    - **Kalıtım** yoluyla **"is-a"** ilişkisini kurarız, yani `Dog` bir `Pet`'tir. Ancak, kalıtımın tam olarak nasıl çalıştığı, **nesne dilimleme** ve **polimorfizm** gibi kavramlarla ilgili daha derin sorular doğurur.
    - `Pet` türündeki bir değişkenin bir `Dog` nesnesine atandığı durum, kalıtım ilişkisini çelişkili hale getirebilir. Çünkü `Pet`, `Dog`'un tüm özelliklerine sahip değildir, sadece temel sınıf üyelerini kabul eder.

### **Sonuç:**

- **Object slicing**, türetilmiş sınıfın nesnesinin, temel sınıf türüne atandığında özel özelliklerin kaybolması durumudur.
- Bu, **nesne yönelimli programlamada dikkat edilmesi gereken bir durumdur**, çünkü türetilmiş sınıfın özel üyeleri kaybolur ve yalnızca temel sınıf üyeleri kalır.
- Kalıtımda **polimorfizm** (farklı türlerdeki nesnelerin aynı türdeymiş gibi işlem görmesi) kullanmak, nesne dilimleme problemini engellemek için daha uygun bir yaklaşımdır.

# **Nesne Dilimleme (Object Slicing) Çözümü:**

1. **Nesne Dilimleme:**
    
    - **Nesne dilimleme**, türetilmiş bir sınıf nesnesinin temel sınıf türündeki bir değişkene atanması sonucu türetilmiş sınıfın özel üyelerinin kaybolmasına neden olur. Bu durum, örneğin `Dog` sınıfından türetilmiş bir nesnenin `Pet` türündeki bir değişkene atanmasıyla meydana gelir.
2. **Dinamik Bellek ve İşaretçiler:**
    
    - **Dinamik bellek** kullanarak, nesneleri heap belleğine yerleştiririz. Bu, nesne türünden bağımsız olarak, nesnenin doğru türünü **işaretçi (pointer)** aracılığıyla yönetmemize olanak tanır.
    - Dinamik bellek ve işaretçiler kullanarak, nesnenin türü ne olursa olsun doğru türe ait üyelere erişilebilir.

### **Dinamik Bellek Kullanımı ve Slicing Çözümü:**

C++'ta, işaretçi (pointer) kullanarak ve nesneleri dinamik olarak ayırarak, nesne dilimleme problemini çözebiliriz. Dinamik bellek kullanmak, nesnenin hangi türe ait olduğunu doğru şekilde izlemenizi sağlar.

### **Örnek: Nesne Dilimleme ve Dinamik Bellek Kullanımı**

```cpp
#include <iostream>
using namespace std;

class Pet {
public:
    string name;
    string breed;

    virtual void printBreed() {
        cout << "Breed: " << breed << endl;
    }
};

class Dog : public Pet {
public:
    string owner;

    void printBreed() override {
        cout << "Breed of " << name << ": " << breed << endl;
    }
};

int main() {
    // Dinamik bellek kullanarak nesneleri yaratma
    Pet* vpet = new Dog(); // Dog türünde bir nesne yaratıyoruz ancak Pet türünde bir işaretçiye atıyoruz
    vpet->name = "Tiny";
    vpet->breed = "Great Dane";

    // Dinamik olarak yaratılmış nesnenin işlevini çağırma
    vpet->printBreed(); // Output: Breed of Tiny: Great Dane

    // Belleği serbest bırakma
    delete vpet;

    return 0;
}
```

### **Açıklamalar:**

1. **Dinamik Bellek Kullanımı (`new` ve `delete`):**
    
    - `Pet* vpet = new Dog();` ifadesi ile dinamik bellek üzerinde bir `Dog` nesnesi yaratıyoruz, ancak bu nesne `Pet` türünde bir işaretçiye atanıyor. Bu, nesne dilimleme problemini çözmek için etkili bir yöntemdir çünkü `vpet` işaretçisi, gerçek türüne bakılmaksızın doğru işlevi çağırabilecektir.
    - Bu tür nesneler için belleği serbest bırakmak için `delete vpet;` komutunu kullanıyoruz.
2. **Polimorfizm ve Sanal Fonksiyonlar (Virtual Functions):**
    
    - `Pet` sınıfındaki `printBreed` fonksiyonu sanal (`virtual`) olarak tanımlanmıştır. Bu sayede, `Pet` türündeki işaretçi ile çağrılan fonksiyon, gerçek nesnenin türüne göre (bu durumda `Dog`) doğru fonksiyonu çağırır. **Polimorfizm** sayesinde, `vpet` işaretçisi doğru `Dog` sınıfındaki `printBreed` fonksiyonunu çağıracaktır.
    - Sonuç olarak, `vpet->printBreed();` ifadesi, **`Dog` sınıfındaki `printBreed` fonksiyonunu** çalıştırır ve doğru tür bilgisi (Great Dane) görüntülenir.
3. **Nesne Dilimleme Sorununun Çözümü:**
    
    - Dinamik bellek ve işaretçiler kullanılarak, **nesne dilimleme** problemi çözülür. Çünkü `vpet` işaretçisi, nesnenin **gerçek türünü** bildiği için, doğru üyelere ve işlevlere erişim sağlar.

### **Sonuç:**

- **Nesne dilimleme** problemi, bir türetilmiş sınıfın nesnesinin temel sınıf türündeki bir değişkene atanması durumunda özel üyelerin kaybolmasına neden olur.
- Bu sorunu çözmek için **dinamik bellek kullanımı** ve **işaretçiler** (pointers) tercih edilebilir. İşaretçiler, nesnenin gerçek türünü doğru şekilde yönetmeye olanak tanır.
- **Polimorfizm** kullanılarak, temel sınıf türündeki işaretçi ile türetilmiş sınıfın doğru fonksiyonları çağrılabilir.

### Dikkat !
C++'ta, **`Pet* ppet`** türündeki bir işaretçi, `Dog* pdog` işaretçisine atanabilir çünkü `Dog` sınıfı, `Pet` sınıfından türetilmiştir. Ancak, işaretçi türü **`Pet*`** olduğu için, işaretçinin gösterdiği nesneye sadece **`Pet`** sınıfının üyelerine erişebilirsiniz. Örneğin `Pet* vpet = new Dog()` yapıldığında `vpet->owner` kullanımı hata verir.

# Virtual Destructors
C++ nesne yönelimli programlamada, sınıf hiyerarşilerinde doğru bir bellek yönetimi yapmak için virtual destructor kullanımı kritik bir öneme sahiptir. Temel problem şudur: Base sınıfın pointer'ı ile Derived sınıfın nesnesini oluşturduğunuzda ve ardından delete işlemi uyguladığınızda, eğer base sınıfın destructor'ı virtual değilse, yalnızca base sınıfın destructor'ı çağrılır.

Örnek vermek gerekirse:

```cpp
class Base {
public:
    ~Base() { // virtual keyword eksik
        std::cout << "Base destructor" << std::endl;
    }
};

class Derived : public Base {
public:
    ~Derived() {
        std::cout << "Derived destructor" << std::endl;
    }
};

int main() {
    Base* pBase = new Derived;
    delete pBase; // Yalnızca Base destructor çağrılır
}
```

Bu durumda Derived sınıfının destructor'ı çağrılmaz, bu da potansiyel bellek sızıntılarına ve yanlış temizleme işlemlerine neden olabilir.

Çözüm basit: Base sınıfın destructor'ını virtual olarak tanımlamak.

```cpp
class Base {
public:
    virtual ~Base() { // virtual keyword eklendi
        std::cout << "Base destructor" << std::endl;
    }
};
```

Virtual destructor kullanarak, delete işlemi sırasında doğru sırayla ve doğru sınıfın destructor'ları çağrılacaktır. Bu, nesne hiyerarşilerinde güvenli ve doğru bellek yönetimi sağlar.

Genel politika olarak, eğer bir sınıfın başka sınıflar tarafından miras alınması bekleniyorsa, destructor'ını virtual olarak tanımlamak iyi bir yaklaşımdır.

# Type-casting
### Upcasting
C++ nesne yönelimli programlamada, sınıf hiyerarşileri arasındaki dönüşümler belirli kurallara tabidir. Temel problem, türetilmiş sınıftan (derived) taban sınıfa (base) veya tam tersi dönüşümlerde nelerin mümkün olup olmadığıdır.

Örneğin, bir Pet sınıfınız ve ondan türeyen bir Dog sınıfınız olduğunu düşünelim:

```cpp
class Pet {
    // Pet sınıfının özellikleri
};

class Dog : public Pet {
    // Dog sınıfına özgü ek özellikler
};
```

Bu örnekte, Dog sınıfı Pet sınıfından türetilmiştir. Dönüşüm kuralları şu şekilde işler:

1. Downcasting (Alt Sınıfa Dönüşüm): `Dog vdog = static_cast<Dog>(vpet);` - Bu işlem illegal'dir. Bir Pet nesnesini doğrudan Dog nesnesine dönüştüremezsiniz. Çünkü her Dog bir Pet'tir, ama her Pet bir Dog değildir.

2. Upcasting (Üst Sınıfa Dönüşüm): `vpet = vdog;` veya `vpet = static_cast<Pet>(vdog);` - Bu işlemler legal'dir. Türetilmiş sınıftan (Dog) taban sınıfa (Pet) dönüşüm sorunsuz gerçekleşir.

Upcasting, nesne yönelimli programlamada oldukça yaygın ve güvenli bir dönüşüm türüdür. Daha spesifik bir sınıftan daha genel bir sınıfa doğru dönüşüm yaparsınız. Bu, polimorfizmin temel mekanizmalarından biridir.

Düşünmeniz gereken temel kural şudur: "Her Dog bir Pet'tir, ama her Pet bir Dog değildir." Bu, dönüşüm kurallarının temelini oluşturur. Downcasting işlemleri için genellikle dynamic_cast gibi güvenli dönüşüm operatörleri kullanılır, ancak bunun için runtime type information (RTTI) gereklidir.

Bu konsept, nesne yönelimli programlamada tür güvenliği ve hiyerarşik ilişkiler açısından kritik bir öneme sahiptir. Doğru kullanıldığında, kodunuzun daha esnek ve genişletilebilir olmasını sağlar.

### Downcasting
Downcasting, taban sınıftan (ancestor) türetilmiş sınıfa (descended) doğru bir dönüşüm işlemidir. Bu işlem oldukça riskli ve tehlikelidir çünkü temel olarak ekstra bilgi varsayımına dayanır. 

C++'ta downcasting genellikle `dynamic_cast` operatörü kullanılarak yapılır. Örnek bir senaryo şöyle olabilir:

```cpp
Pet *ppet = new Dog;  // Pet pointer'ı Dog nesnesini gösteriyor
Dog *pdog = dynamic_cast<Dog*>(ppet);  // Downcasting işlemi
```

Bu işlem yasal görünse de, ciddi riskleri vardır:

1. Ekstra Bilgi Varsayımı: Downcasting, türetilmiş sınıfın taban sınıftan daha fazla bilgi içerdiğini varsayar. Ancak bu her zaman doğru olmayabilir.

2. Güvenlik Sorunları: Eğer dönüşüm güvenli değilse, `dynamic_cast` null pointer döndürecektir.

3. Karmaşık Takip Gereksinimleri: Eklenecek tüm bilgilerin ve üye fonksiyonların izlenmesi gerekir.

Downcasting'in güvenli olması için bazı önemli kurallar vardır:
- Tüm üye fonksiyonların virtual olarak tanımlanması
- Sınıf hiyerarşisinin net bir şekilde tasarlanması
- Runtime Type Information (RTTI) desteğinin sağlanması

Pratikte, downcasting nadiren kullanılır çünkü:
- Kodun tasarımında zayıflıklara işaret edebilir
- Performans maliyeti yüksektir
- Nesne yönelimli tasarım prensiplerine aykırı olabilir

Genellikle, iyi bir nesne yönelimli tasarımda downcasting'e gerek kalmaz. Bunun yerine, polimorfizm ve sanal fonksiyonlar tercih edilir.

Eğer mutlaka downcasting kullanmak gerekiyorsa, çok dikkatli olunmalı ve alternatif tasarım yaklaşımları düşünülmelidir.

# Özet Kod
```cpp
#include <iostream>
using namespace std;

// Base class
class Pet {
public:
    string name;
    virtual void makeSound() const {
        cout << "Pet makes a sound" << endl;
    }
    virtual ~Pet() {
        cout << "Pet destructor" << endl;
    }
};

// Derived class
class Dog : public Pet {
public:
    string breed;
    void makeSound() const override {
        cout << "Dog barks" << endl;
    }
    ~Dog() {
        cout << "Dog destructor" << endl;
    }
};

int main() {
    // Upcasting: Derived class object to Base class pointer
    Pet* ppet = new Dog();
    ppet->name = "Buddy";
    ppet->makeSound(); // Calls Dog's makeSound() due to virtual function

    // Downcasting: Base class pointer to Derived class pointer
    Dog* pdog = dynamic_cast<Dog*>(ppet);
    if (pdog) {
        pdog->breed = "Golden Retriever";
        cout << "Dog's breed: " << pdog->breed << endl;
    } else {
        cout << "Downcasting failed" << endl;
    }

    // Object slicing
    Pet vpet;
    Dog vdog;
    vdog.name = "Max";
    vdog.breed = "German Shepherd";
    vpet = vdog; // Object slicing occurs here
    cout << "vpet name: " << vpet.name << endl;
    // cout << "vpet breed: " << vpet.breed << endl; // ERROR: breed is sliced off

    // Virtual destructor
    delete ppet; // Calls both Pet and Dog destructors due to virtual destructor

    return 0;
}
```

Daha fazla bilgi için: [[15.01 - Polymorphism Extra]]