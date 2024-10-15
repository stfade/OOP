*Links*: [[00 - Index|Index]]
*Date*: 01.10.2024
*Resources*: [name]()

---
# Predefined Functions
* Matematik fonskiyonları `cmath` kütüphanesinde bulunur.
* Bu fonskiyonlar `cstdlib` kütüphanesinde bulunur
```cpp
	 abs() // Returns absolute value of an int
     labs() // Returns absolute value of a long int
     *fabs() // Returns absolute value of a float
```
* `pow(x,y)` -> x'in y'inci kuvvetini döndürür (double alır, double döndürür). 
* `sqrt(x)` -> x'in kök değerini döndürür (double alır, double döndürür). **![C:\WINDOWS\Desktop\Oh_type\sacitch_C++_ppt\gif\savitchc03d02_2of2.gif](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUdEbuuadqPkWPa68yWdDm7hUI6bsJiXxvmWx4o8xPhHuR0bAFqtHRb3QOZxIrdqA91JWh9XP1EWzW23JuoeEzHzOr9uZm6lERufEf-jPPBxrsHOAKDLPWMBefT5XW7J6kz8RkhQJ5uUnXwRvojZobpF6WAoVoMowy0vC7Ph18Hwl2O5cyhOzmE=s2048?key=vW0pEVkiRzCdUZhLpUXvDw)**
* srand:
	```cpp
	#include <iostream>
	#include <cstdlib> // srand ve rand için gerekli
	#include <ctime>   // time için gerekli
	
	int main() {
	    // Rastgele sayı üreticisinin başlangıç değerini ayarla
	    srand(static_cast<unsigned int>(time(0)));
	
	    // Rastgele bir sayı üret ve ekrana yazdır
	    int random_number = rand();
	    std::cout << "Random Number: " << random_number << std::endl;
	
	    return 0;
	}
	```
* 
# Programmer-defined Functions
* `main` fonksiyonunu işletim sistemi çağırır.
* İki tip fonksiyon vardır. Değer döndüren ya da hiçbir şey döndürmeyen.
* Fonksiyonlarda bir işin nasıl yapıldığı bilgisi, fonksiyonu dışarıdan çağıran için önemli değildir.
# Scope Rules
 * Global data sabitler (constants) için kullanılmalıdır.
 * [[03.01 - Parameters and Arguments|Parameters and Arguments]]: Parametreler fonksiyonun tanımındaki değişkenlere verilen isimdir. Argümanlar fonskiyonda kullanılacak değerlerdir.