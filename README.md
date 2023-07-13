# SOLID

# S = Single Responsibility Principle(SRP)

### A module should be responsible to one, and only one, actor. [2] '(Robert Cecil Martin, 2017)'

setiap class dipisahkan berdasarkan fungsionalitasnya dan hanya akan menangani satu tanggung jawab (fungsi).

### Tanpa (SRP)
```dart
class Order {
  void calculeteTotalSum() {}
  void getItems() {}
  void getItemCount() {}
  void addItem(Item item) {}
  void deleteItem(Item item) {}
  void printOrder() {}
  void showOrder() {}
  void getDailyHistory() {}
  void getMonthlyHistory() {}
}
class Item {}

```
 

## (SRP)
```dart
class Order {
  void calculateTotalSum() {}
  void getItems() {}
  void getItemCount() {}
  void addItem(Item item) {}
  void deleteItem(Item item) {}
}
 
class Item {}
 
class OrderHistory {
  void getDailyHistory() {}
  void getMonthlyHistory() {}
}
 
class OrderViewer {
  void printOrder(Order order) {}
  void showOrder(Order order) {}
}
```
<img src="https://github.com/msarifin29/solid/blob/main/S.jpeg" width="350" height="700" />


# O = Open/Close Principle (OCP)

## "A software artifact should be open for extension but closed for modification." [2] (Bertrand Meyer, 1988)

Sebuah artefak perangkat lunak harus terbuka untuk ditambahkan 
tetapi tertutup untuk dimodifikasi. 

### Tanpa (OCP)
```dart
class CinemaCalculations {
  double calculateAdminFee(Cinema cinema) {
    if (cinema is StandardCinema) {
      return cinema.price * 10 / 100;
    } else if (cinema is DeluxeCinema) {
      return cinema.price * 12 /100;
    } else if (cinema is PremiumCinema) {
      return cinema.price * 20 / 100;
    } else {
      return 0.0;
    }
  }
}
```

## (OCP)
```dart
class Cinema {
  double price;
  Cinema(this.price);
}
 
class StandardCinema extends Cinema {
  StandardCinema(double price) : super(price);
}
 
class DeluxeCinema extends Cinema {
  DeluxeCinema(double price) : super(price);
}
 
class PremiumCinema extends Cinema {
  PremiumCinema(double price) : super(price);
}
```
<img src="https://github.com/msarifin29/solid/blob/main/O.jpeg" width="350" height="700" />


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


# I = Interface Segregation Principle (ISP)

## "Clients should not be forced to depend upon interfaces that they do not use." (Robert Cecil Martin)

Prinsip ini sendiri bertujuan untuk mengurangi jumlah ketergantungan sebuah 
class terhadap interface class yang tidak dibutuhkan.

### Tanpa (ISP)
```dart
abstract class VehicleInterface {
  void drive();
  void stop();
  void refuel();
  void openDoors();
}
 
class MotorCycle implements VehicleInterface {
  @override
  void drive() {}
 
  @override
  void refuel() {}
 
  @override
  void stop() {}
 
  // Can not be implemented
  @override
  void openDoors() {}
}
```

### (ISP)
```dart
abstract class VehicleInterface {
  void drive();
  void stop();
  void refuel();
}
 
abstract class DoorInterface {
  void openDoors();
}

class Motorcycle implements VehicleInterface {
  @override
  void drive() {
    // TODO: implement drive
  }
 
  @override
  void refuel() {
    // TODO: implement refuel
  }
 
  @override
  void stop() {
    // TODO: implement stop
  }
}
class Car implements VehicleInterface, DoorInterface {
  @override
  void drive() {
    // TODO: implement drive
  }
 
  @override
  void refuel() {
    // TODO: implement refuel
  }
 
  @override
  void stop() {
    // TODO: implement stop
  }
 
  @override
  void openDoors() {
    // TODO: implement openDoors
  }
}
```
<img src="https://github.com/msarifin29/solid/blob/main/I.jpeg" width="350" height="700" />


# D = Dependency Inversion Principle (DIP)

## "High-level modules should not depend on low-level modules. Both should depend on abstractions." (Robert Cecil Martin)

Prinsip Dependency Inversion hampir sama dengan konsep layering dalam aplikasi, 
di mana low-level modules bertanggung jawab dengan fungsi yang sangat detail dan 
high-level modules menggunakan low-level classes untuk mencapai tugas yang lebih besar. 
Hal ini bisa dicapai dengan bergantung pada sebuah abstraksi, ketika ada ketergantungan 
antar kelas seperti interface, daripada referensi langsung ke kelas lainnya.

### Tanpa (DIP)
```dart
class Car {
  final Engine _engine;
  Car(this._engine);
 
  void start() {
    _engine.start();
  }
}
 
class Engine {
  void start() {
 
  }
}

class DieselEngine {
  void start() {
 
  }
}
```

### (DIP)
```dart
abstract class EngineInterface {
  void start();
}
class Car {
  final EngineInterface _engine;
 
  Car(this._engine);
 
  void start() {
    _engine.start();
  }
}
class PetrolEngine implements EngineInterface {
  @override
  void start() {
    // TODO: implement start
  }
}
 
class HybridEngine implements EngineInterface {
  @override
  void start() {
    // TODO: implement start
  }
}
 
class DieselEngine implements EngineInterface {
  @override
  void start() {
    // TODO: implement start
  }
}
void main() {
  final petrolEngine = PetrolEngine();
  final petrolCar = Car(petrolEngine);
 
  final dieselEngine = DieselEngine();
  final dieselCar = Car(dieselEngine);
 
  final hybridEngine = HybridEngine();
  final hybridCar = Car(hybridEngine);
 
  petrolCar.start();
  dieselCar.start();
  hybridCar.start();
}
```

<img src="https://github.com/msarifin29/solid/blob/main/D.jpeg" width="350" height="700" />
