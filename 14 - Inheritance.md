*Links*: [[00 - Index]]
*Date*: 19.11.2024
*Resources*: [name]()

---
Nesne yönelimli programlama, güçlü bir programlama tekniğidir. Bu teknik, kalıtım adı verilen bir soyutlama boyutu sağlar. Bir sınıfın genel formu tanımlanır ve ardından bu genel sınıfın özelliklerini miras alan özel versiyonlar oluşturulur. Bu özel versiyonlar, genel sınıfın işlevselliğini kendi uygun kullanımları için ekler veya değiştirir.
# Inheritance Basics
- Yeni bir sınıf, başka bir sınıftan miras alınır. Temel sınıf, diğerlerinin türetildiği "genel" sınıftır. Türemiş sınıf ise yeni sınıftır. Bu yeni sınıf, otomatik olarak temel sınıfın üye değişkenlerine ve üye fonksiyonlarına sahip olur. Ardından, ek üye fonksiyonları ve değişkenler ekleyebilir.
- Örneğin, "Çalışanlar" sınıfını ele alalım. Bu sınıf, maaşlı çalışanlar ve saatlik çalışanlardan oluşur. Her biri, çalışanların bir "alt kümesi"dir. Bir diğer alt küme ise her ay veya hafta sabit ücret alan çalışanlar olabilir.
- Genel bir "çalışan" türüne ihtiyaç duyulmaz çünkü kimse sadece bir "çalışan" değildir. Ancak, çalışan kavramı faydalıdır. Tüm çalışanların isimleri ve sosyal güvenlik numaraları vardır. Bu temel bilgilerle ilgili fonksiyonlar tüm çalışanlar arasında aynıdır. Bu nedenle, "genel" sınıf, çalışanlarla ilgili tüm bu "şeyleri" içerebilir.
- "Çalışan" sınıfının birçok üyesi, tüm çalışan türlerine uygulanır. Erişimci fonksiyonlar ve değiştirici fonksiyonlar gibi. Çoğu veri öğesi, örneğin sosyal güvenlik numarası (SSN), isim ve maaş gibi. Ancak, bu sınıfın "nesneleri" olmayacaktır.
- `printCheck()` fonksiyonunu düşünelim: Bu fonksiyon her zaman türemiş sınıflarda yeniden tanımlanacaktır, böylece farklı çalışan türleri farklı çekler alabilir. "Farklılaştırılmamış" bir çalışan için gerçekten mantıklı değildir. Bu nedenle, `Employee` sınıfındaki `printCheck()` fonksiyonu sadece bir hata mesajı verir: "printCheck called for undifferentiated employee!! Aborting…"

İşte yukarıdaki açıklamaları özetleyen bir kod örneği:

```cpp
#include <iostream>
#include <string>

// Temel sınıf
class Employee {
public:
    std::string name;
    std::string ssn;

    Employee(std::string n, std::string s) : name(n), ssn(s) {}

    virtual void printCheck() {
        std::cerr << "printCheck called for undifferentiated employee!! Aborting…" << std::endl;
    }
};

// Türemiş sınıf: Maaşlı çalışan
class SalariedEmployee : public Employee {
public:
    double salary;

    SalariedEmployee(std::string n, std::string s, double sal) : Employee(n, s), salary(sal) {}

    void printCheck() override {
        std::cout << "Printing check for salaried employee: " << name << std::endl;
    }
};

// Türemiş sınıf: Saatlik çalışan
class HourlyEmployee : public Employee {
public:
    double hourlyRate;
    int hoursWorked;

    HourlyEmployee(std::string n, std::string s, double rate, int hours) 
        : Employee(n, s), hourlyRate(rate), hoursWorked(hours) {}

    void printCheck() override {
        std::cout << "Printing check for hourly employee: " << name << std::endl;
    }
};

int main() {
    SalariedEmployee salaried

("John Doe", "123-45-6789", 50000);
    HourlyEmployee hourly("Jane Smith", "987-65-4321", 20, 40);

    salaried.printCheck();
    hourly.printCheck();

    return 0;
}
```

Bu kod örneğinde, `Employee` temel sınıfı ve ondan türetilen `SalariedEmployee` ve `HourlyEmployee` sınıfları gösterilmektedir. Her iki türemiş sınıf da `printCheck()` fonksiyonunu yeniden tanımlar.

Aile ilişkilerini simüle etmek yaygındır. Ebeveyn sınıf, temel sınıfa atıfta bulunur. Çocuk sınıf, türemiş sınıfa atıfta bulunur. Ata sınıf, bir ebeveynin ebeveyni olan sınıftır. Torun sınıf, ata sınıfının tersidir. 

Bu kavramları bir kod örneği ile gösterelim:

```cpp
#include <iostream>
#include <string>

// Ata sınıf
class Person {
public:
    std::string name;

    Person(std::string n) : name(n) {}

    virtual void display() {
        std::cout << "Name: " << name << std::endl;
    }
};

// Ebeveyn sınıf
class Employee : public Person {
public:
    std::string ssn;

    Employee(std::string n, std::string s) : Person(n), ssn(s) {}

    void display() override {
        std::cout << "Name: " << name << ", SSN: " << ssn << std::endl;
    }
};

// Çocuk sınıf
class Manager : public Employee {
public:
    double salary;

    Manager(std::string n, std::string s, double sal) : Employee(n, s), salary(sal) {}

    void display() override {
        std::cout << "Name: " << name << ", SSN: " << ssn << ", Salary: " << salary << std::endl;
    }
};

int main() {
    Person person("John Doe");
    Employee employee("Jane Smith", "123-45-6789");
    Manager manager("Alice Johnson", "987-65-4321", 75000);

    person.display();
    employee.display();
    manager.display();

    return 0;
}
```

Bu örnekte, `Person` ata sınıfı, `Employee` ebeveyn sınıfı ve `Manager` çocuk sınıfı olarak tanımlanmıştır. Her sınıf, `display()` fonksiyonunu yeniden tanımlar.

- Temel sınıf yapıcıları, türemiş sınıflarda miras alınmaz! Ancak, türemiş sınıf yapıcısı içinde çağrılabilirler ve bu bizim için yeterlidir. Temel sınıf yapıcısı, temel sınıfın tüm üye değişkenlerini başlatmalıdır. Bu değişkenler türemiş sınıf tarafından miras alınır. Bu nedenle, türemiş sınıf yapıcısı, temel sınıf yapıcısını çağırır ve bu, türemiş sınıf yapıcısının yaptığı "ilk" şeydir.

- Türemiş sınıf yapıcısı her zaman temel sınıfın yapıcılarından birini çağırmalıdır. Eğer çağırmazsanız, varsayılan temel sınıf yapıcısı otomatik olarak çağrılır.

Türemiş sınıf, özel üye değişkenlerini miras alır, ancak bunlara doğrudan erişemez. Türemiş sınıfın üye fonksiyonları bile bu özel üye değişkenlerine doğrudan erişemez. Özel üye değişkenlerine yalnızca tanımlandıkları sınıfın üye fonksiyonları aracılığıyla "isimle" erişilebilir.

Bir kod örneği ile açıklayalım:

```cpp
#include <iostream>
#include <string>

// Temel sınıf
class Employee {
private:
    std::string name;
    std::string ssn;

public:
    Employee(std::string n, std::string s) : name(n), ssn(s) {}

    std::string getName() const {
        return name;
    }

    std::string getSSN() const {
        return ssn;
    }
};

// Türemiş sınıf
class HourlyEmployee : public Employee {
private:
    double wageRate;
    double hours;

public:
    HourlyEmployee(std::string theName, std::string theNumber, double theWageRate, double theHours)
        : Employee(theName, theNumber), wageRate(theWageRate), hours(theHours) {}

    void display() {
        // Özel üye değişkenlerine doğrudan erişim yok
        std::cout << "Name: " << getName() << ", SSN: " << getSSN()
                  << ", Wage Rate: " << wageRate << ", Hours: " << hours << std::endl;
    }
};

int main() {
    HourlyEmployee hourly("Jane Smith", "987-65-4321", 20.0, 40.0);
    hourly.display();

    return 0;
}
```

Bu örnekte, `Employee` sınıfındaki `name` ve `ssn` özel üye değişkenlerine doğrudan erişim yoktur. `HourlyEmployee` sınıfı, bu değişkenlere `getName()` ve `getSSN()` üye fonksiyonları aracılığıyla erişir.

- Temel sınıfın üye fonksiyonları da aynı şekilde davranır. Temel sınıfın üye fonksiyonları, temel sınıfın arayüzü ve uygulaması dışında erişilemez. Türemiş sınıfın üye fonksiyon tanımlarında bile doğrudan erişilemezler.
- C++'da sınıf üyeleri üç ana erişim belirteci ile tanımlanabilir: `public`, `private`, ve `protected`. [[14.01 - Protected]] 

- C++'da türetilmiş sınıfların arayüzünü (interface) anlamak için, temel sınıftan (base class) türetilen sınıfın (derived class) nasıl davranacağını ve hangi üyelerin nasıl kullanılacağını bilmek önemlidir.

	1. **Türetilmiş Sınıfın Arayüzü:**
		 - **Yeni Üye Fonksiyonların Bildirimi:** Türetilmiş sınıf, temel sınıftan farklı olarak kendi üye fonksiyonlarını tanımlayabilir. Bu fonksiyonlar, türetilmiş sınıfın özgün işlevselliğini sağlar.
		 - **Miras Alınan Üye Fonksiyonların Bildirimi:** Türetilmiş sınıf, temel sınıftan miras aldığı üye fonksiyonların bazılarını yeniden tanımlayabilir (override). Bu, türetilmiş sınıfın miras aldığı fonksiyonların davranışını değiştirmesine olanak tanır.
	2. **Miras Alınan Üye Fonksiyonların Değiştirilmemesi:**
		- **Değiştirilmemiş Fonksiyonlar:** Türetilmiş sınıf, temel sınıftan miras aldığı üye fonksiyonları yeniden tanımlamazsa, bu fonksiyonlar otomatik olarak değiştirilmeden türetilmiş sınıfa aktarılır.
	3. Türetilmiş Sınıfın Uygulaması:
		- **Yeni Üye Fonksiyonların Tanımlanması:** Türetilmiş sınıf, kendi üye fonksiyonlarının uygulamasını sağlar. Bu, türetilmiş sınıfın özgün işlevselliğini gerçekleştirir.
		- **Miras Alınan Fonksiyonların Yeniden Tanımlanması:** Türetilmiş sınıf, temel sınıftan miras aldığı üye fonksiyonların bazılarını yeniden tanımlayarak, bu fonksiyonların davranışını değiştirir.

- **Yeniden Tanımlama:** Türetilen sınıfta, temel sınıfta var olan bir fonksiyonu aynı parametre listesi ile yeniden tanımlamaktır. Overload ise aynı isimde fonksiyonları farklı parametre listeleri ile tanımlamaktır.
- C++'da function signature şunlar ile oluşturulur:
	- Fonksiyon adı
	- Parametrelerin sayısı ve tiplerinin sırası
- Function signature şunları içermez:
	- Return type
	- const keyword
	- Referance operatörü (&)
- **Base Class fonksiyonunun çağırılması:** Türetilmiş sınıfta bir fonksiyonu yeniden tanımladığınızda, temel sınıfın orijinal fonksiyonu hala mevcuttur. Bu fonksiyonu, `::` operatörünü kullanarak açıkça çağırabilirsiniz.
- C++'da, temel sınıftaki "normal" fonksiyonlar türetilmiş sınıfa miras olarak aktarılır. Ancak, bazı özel fonksiyonlar bu kuralın dışındadır. Bu özel fonksiyonlar arasında kurucu fonksiyonlar (constructors), yıkıcı fonksiyonlar (destructors), kopyalama kurucusu (copy constructor) ve atama operatörü (assignment operator) bulunur.
- C++'da, temel sınıfın yıkıcı fonksiyonu (`destructor`) doğru bir şekilde çalışıyorsa, türetilmiş sınıfın yıkıcı fonksiyonunu yazmak oldukça kolaydır. Türetilmiş sınıfın yıkıcı fonksiyonu çağrıldığında, otomatik olarak temel sınıfın yıkıcı fonksiyonu da çağrılır. Bu nedenle, türetilmiş sınıfın yıkıcı fonksiyonunda temel sınıfın yıkıcı fonksiyonunu açıkça çağırmanıza gerek yoktur. Önce türetilen sınıf yok edilir daha sonra temel sınıf yok edilir.
- C++'da, türetilmiş sınıfların yıkıcı fonksiyonları (destructors), nesne kapsam dışına çıktığında veya silindiğinde otomatik olarak çağrılır. Yıkıcı fonksiyonların çağrılma sırası, kurucu fonksiyonların (constructors) çağrılma sırasının tersidir. Yani, en türetilmiş sınıfın yıkıcı fonksiyonu ilk olarak çağrılır ve ardından temel sınıfların yıkıcı fonksiyonları sırayla çağrılır.
# Is-a / Has-a Relationship
C++'da kalıtım (inheritance) ve bileşen (composition) kavramları, sınıflar arasındaki ilişkileri tanımlamak için kullanılır. Bu ilişkiler, "Is a" ve "Has a" olarak adlandırılan iki temel kategoride incelenebilir.
- **"Is a" İlişkisi:** Kalıtım, bir sınıfın başka bir sınıftan türetilmesi anlamına gelir. Bu, türetilmiş sınıfın temel sınıfın bir özelliğini taşıdığını veya temel sınıfın bir türü olduğunu gösterir.
```cpp
class Employee {
public:
    void printDetails() {
        std::cout << "Employee details" << std::endl;
    }
};

class HourlyEmployee : public Employee {
public:
    void printHourlyDetails() {
        std::cout << "HourlyEmployee details" << std::endl;
    }
};

int main() {
    HourlyEmployee he;
    he.printDetails();       // Employee'nin fonksiyonu
    he.printHourlyDetails(); // HourlyEmployee'nin fonksiyonu
    return 0;
}
```
- **"Has a" İlişkisi:** Bileşen, bir sınıfın başka bir sınıfın nesnesini üye veri (member data) olarak içermesi anlamına gelir. Bu, bir sınıfın başka bir sınıfın bir parçası olduğunu gösterir.
```cpp
class Engine {
public:
    void start() {
        std::cout << "Engine started" << std::endl;
    }
};

class Car {
private:
    Engine engine;
public:
    void startCar() {
        engine.start();
        std::cout << "Car started" << std::endl;
    }
};

int main() {
    Car car;
    car.startCar();  // Car'ın fonksiyonu
    return 0;
}
```

# Protected ve Private Kalıtım
C++'da, kalıtımın iki özel formu bulunur: `protected` kalıtım ve `private` kalıtım. Bu iki form, genellikle sık kullanılmaz ve standart `public` kalıtıma göre daha az yaygındır. Bu formların nasıl çalıştığını ve ne zaman kullanılabileceğini anlatacağım.
-  `protected` kalıtımda, temel sınıfın `public` üyeleri, türetilmiş sınıfta `protected` olarak kabul edilir. Bu, türetilmiş sınıfın bu üyelere erişebilmesini sağlar, ancak bu üyeler dışarıdan erişilemez hale gelir.
```cpp
class Employee {
public:
    void printDetails() {
        std::cout << "Employee details" << std::endl;
    }
};

class SalariedEmployee : protected Employee {
public:
    void printSalariedDetails() {
        printDetails();  // protected olarak erişilebilir
    }
};

int main() {
    SalariedEmployee se;
    se.printSalariedDetails();  // Çıktı: Employee details
    // se.printDetails();  // Hata: printDetails() artık protected
    return 0;
}
```

- `private` kalıtımda, temel sınıfın tüm üyeleri, türetilmiş sınıfta `private` olarak kabul edilir. Bu, türetilmiş sınıfın bu üyelere erişebilmesini sağlar, ancak bu üyeler dışarıdan veya başka türetilmiş sınıflardan erişilemez hale gelir.
```cpp
class Employee {
public:
    void printDetails() {
        std::cout << "Employee details" << std::endl;
    }
};

class SalariedEmployee : private Employee {
public:
    void printSalariedDetails() {
        printDetails();  // private olarak erişilebilir
    }
};

int main() {
    SalariedEmployee se;
    se.printSalariedDetails();  // Çıktı: Employee details
    // se.printDetails();  // Hata: printDetails() artık private
    return 0;
}
```

# Çoklu Kalıtım
C++'da, bir türetilmiş sınıfın birden fazla temel sınıfa sahip olması mümkündür. Bu durum, çoklu kalıtım (multiple inheritance) olarak adlandırılır. Çoklu kalıtım, bir sınıfın birden fazla temel sınıftan miras almasını sağlar, ancak bu durumda belirsizlikler (ambiguities) ve karmaşıklıklar ortaya çıkabilir. Bu nedenle, çoklu kalıtım dikkatli kullanılmalıdır ve genellikle deneyimli programcılar tarafından tercih edilir.
- Bir türetilmiş sınıf, birden fazla temel sınıftan miras alabilir. Bu durumda, temel sınıflar virgülle ayrılarak belirtilir.
```cpp
#include <iostream>

// Temel Sınıf 1
class Base1 {
public:
    void displayBase1() {
        std::cout << "Base1 display" << std::endl;
    }
};

// Temel Sınıf 2
class Base2 {
public:
    void displayBase2() {
        std::cout << "Base2 display" << std::endl;
    }
};

// Türetilmiş Sınıf
class DerivedMulti : public Base1, public Base2 {
public:
    void displayDerived() {
        std::cout << "DerivedMulti display" << std::endl;
    }
};

int main() {
    DerivedMulti dm;
    dm.displayBase1();   // Base1'in fonksiyonu
    dm.displayBase2();   // Base2'nin fonksiyonu
    dm.displayDerived(); // DerivedMulti'nin fonksiyonu
    return 0;
}
```
- Eğer iki temel sınıf aynı isimli bir üye içeriyorsa, türetilmiş sınıfta bu üyeye erişirken belirsizlik oluşabilir. Bu durumda, hangi temel sınıfın üyesine erişileceğini belirtmek için kapsam çözünürlük operatörü (`::`) kullanılmalıdır.
```cpp
#include <iostream>

// Temel Sınıf 1
class Base1 {
public:
    void display() {
        std::cout << "Base1 display" << std::endl;
    }
};

// Temel Sınıf 2
class Base2 {
public:
    void display() {
        std::cout << "Base2 display" << std::endl;
    }
};

// Türetilmiş Sınıf
class DerivedMulti : public Base1, public Base2 {
public:
    void displayDerived() {
        Base1::display();  // Base1'in display fonksiyonu
        Base2::display();  // Base2'nin display fonksiyonu
    }
};

int main() {
    DerivedMulti dm;
    dm.displayDerived();
    return 0;
}
```


**Alternatif Yaklaşımlar:**
- **Bileşen (Composition):** Çoklu kalıtım yerine, bileşen kullanarak sınıflar arasındaki ilişkileri daha basit bir şekilde yönetmek mümkündür.
- **Arayüzler (Interfaces):** C++'da arayüzler olmamasına rağmen, saf sanal fonksiyonlar (pure virtual functions) kullanarak benzer bir yapı oluşturulabilir.