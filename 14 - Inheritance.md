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
# Programming with Inheritance