# L = Liskov Substitution Principle (LSP)

## “If for each object o1 of type S there is an object o2 of type T such that for  all programs P defined in terms of T, the behaviour of P is unchanged when o1 is substituted for o2 then S is a subtype of T.” [2] (Barbara Liskov, 1988)

Sederhananya, Liskov’s substitution adalah aturan yang berlaku untuk hirarki 
pewarisan.  Hal ini mengharuskan kita untuk mendesain kelas-kelas yang kita
 miliki sehingga ketergantungan antar klien dapat disubstitusikan tanpa klien 
 mengetahui tentang perubahan yang ada. Oleh karena itu, seluruh SubClass 
 setidaknya dapat berjalan dengan cara yang sama seperti SuperClass-nya.

### Tanpa (LSP)
```dart
abstract class Product {
    String getName();
    DateTime getExpiredDate();
 
    // Function to get all of information about [Product]
    void getProductInfo() {
        // some magic code
    }
}
 
class Vegetable extends Product {
    @override
    String getName() {
        return 'Broccoli';
    }
 
    @override
    DateTime getExpiredDate() {
        return DateTime.now();
    }
}
 
class Smartphone extends Product {
    @override
    String getName() {
        return 'Samsung S10+ Limited Edition';
    }
 
    @override
    DateTime getExpiredDate() {
        return DateTime.now();  // ???????
    }
}
```

### (LSP)
```dart
abstract class Product {
    String getName();
 
    //Function to get all of information about [Product]
    void getProductInfo() {
        // some magic code
    }
}
 
abstract class FoodProduct extends Product {
    DateTime getExpiredDate();
}
 
class Vegetable extends FoodProduct {
    @override
    String getName() {
        return 'Broccoli';
    }
 
    @override
    DateTime getExpiredDate() {
        return DateTime.now();
    }
}

class Smartphone extends Product {
    @override
    String getName() {
        return 'Samsung S10+ Limited Edition';
    }
}
```

<img src="https://github.com/msarifin29/solid/blob/main/L.png" width="350" height="700" />
