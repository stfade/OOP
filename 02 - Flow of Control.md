*Links*: [[00 - Index|Index]]
*Date*: 01.10.2024
*Resources*: [name]()

---
# Boolean Expressions
### Logical Operators
**![C:\WINDOWS\Desktop\Oh_type\sacitch_C++_ppt\gif\savitchc02d01.gif](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUfboJi7t-Tepic6ri4QEa6x-jckxfo_KYGRfueXdi6FZoY4ua0VDFRRGdKOWAApe9O1wrRcSSU3l-hEUGlo9VZHL9WJjsGSQSXJvQj_qvlWtztqD6n-rJrBIPrkerl0nBQgvgfFF01z1FtEowocKtCS8JXJjivasFttjEjTdI4Qyw=s2048?key=cmT7p7BGjJt0jRtdW9yifw)**

### Bool Type
* True ya da false değeri döndürür.
### Precedence Operators (Yüksek öncelikten düşüğe doğru)
* [[02.01 - Scope Resolution Operator|Scope Resolution Operator]] `::`
* Dot Operator `.` `myObject.myMethod();`
* Member Selection `->` `myObject.myMember = 10;`
* Array Indexing `[]`
* Function Call `()`
* Postfix Increment `a++`
* Postfix Decrement `a--`
* Prefix Increment `++a`
* Prefix Decrement `--a`
* Not `!`
* Unary Minus `-`
* Unary Plus `+`
* Dereference `*`
* Address of `&`
* Create (allocate memory) `new`
* Destroy (deallocate memory) `delete`
* Destroy array (deallocate) `delete[]`
* Size of object `sizeof`
* Type cast `()`
* Multiply `*`
* Divide `/`
* Remainder (Mod) `%`
* Addition `+`
* Subtraction `-`
* Insertion (output) `<<`
* Extraction (input) `>>`
* Conditional Operator ` ? : ` `int max = (a > b) ? a : b;`
* Throw an exception `throw`
	```cpp
	#include <iostream>
	#include <stdexcept> // std::invalid_argument için gerekli
	  
	int divide(int a, int b) {
		if (b == 0) {
			throw std::invalid_argument("Division by zero is not allowed");
		}
		return a / b;
	}
	
	int main() {
		try {
			int result = divide(10, 0);
			std::cout << "Result: " << result << std::endl;
		} catch (const std::invalid_argument& e) {
			std::cerr << "Error: " << e.what() << std::endl;
		}
		return 0;
	}
	```
* 

# Branching Mechanisms
- if-else, switch
- switch statement great for menus
# Loops
* `for`
* `while`
* `do while`
# Intro to File Input
*  `fstream` kütüphanesi kullanılır.
	```cpp
		#include <fstream>  
		using namespace std;
	```
* Kullanmak için bir `ifstream` objesi oluşturulur.
	```cpp
		ifstream inputStream;
	```
* Sonra bu değişkene bir dosya bağlanır.
	```cpp
		inputStream.open("filename.txt");
	```
* Bu şekilde dosyadan okuma yapılır.
	```cpp
		inputStream >> var;
	```
* Bu şekilde de dosya kapatılır.
	```cpp
		inputStream.close();
	```
* Örnek kod:
	**![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUdulxzEcKePLhmNFOrr_syEJd1Z5QueytWy4j9spQkNL-VteicU8y0BT4fUZlJphCHDDqsvxuES5zb5CMAi1GHtSdZPbSpXo-plqjQzdMfnljXTBB4vgFJWLsrTpvNKO4d3nkhcqwoYo9RZkZw0hARkCasdSh1UZlNvcxqtPFT7=s2048?key=cmT7p7BGjJt0jRtdW9yifw)**
