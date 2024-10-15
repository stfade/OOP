*Links*: [[00 - Index|Index]]
*Date*: 10.10.2024
*Resources*: [name]()

---
# Introduction to Arrays
* Aynı tipteki veri grubudur.
* Bir liste olarak da kullanılır.
* C'deki arrayler'den pek bir farkı yoktur.
### Declaring and Referencing Arrays
* Bir array tanımlandığında, bellekte bu array'in boyutu kadar yer açılır.
* Örneğin `int a[5]` dendiğinde bellekte 20 byte yer ayrılır. (integer'ın 4 byte olduğu sistemlerde)
### For-loops and Arrays
### Arrays in memory
* Diziler 0'dan başlar. Bunun nedeni şudur. `a[1]` aslında `*(a+1)` şeklinde compile edilir. `a[1]` demek, bellekte `a` adresinin 1 fazlasındaki yeri ifade eder. Yani bir hesaplama yapılır. `a[0]` demek `*(a+0)` olduğu için `a` nın bulunduğu yerdeki elemana, yani ilk elemana bu şekilde erişilir. Index'ler bu gibi sebeplerden dolayı 0'dan başlar. Detaylı bilgi için [[05.01 - Index'ler Neden 0'dan Başlar]]'ı inceleyin.
* C++'da array'lerin sınırları dışına çıkılmaya izin verilir. Bu yüzden range'in dışına çıkılma konusunda dikkatli olmak gerekir.
* Dizilerin indexlerindeki veriler bellekte ardışık olarak sıralanır. (Sequentially Allocated)
# Arrays in Functions
* Bir fonksiyona array yollandığında, aslında array'in başlangıç adresi yollanır. Bu yüzden parametre olarak `int *arr` ile `int arr[]` arasında bir fark yoktur. Derleyici, her iki durumda da parametreyi bir işaretçi olarak değerlendirir.
### Arrays as Function Arguments, Return Values
# Programming with Arrays
### Partially Filled Arrays, Searching, Sorting
# Multidimensional Arrays