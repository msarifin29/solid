D = Dependency Inversion Principle (DIP)

"High-level modules should not depend on low-level modules. Both should depend on abstractions." 
(Robert Cecil Martin)

Prinsip Dependency Inversion hampir sama dengan konsep layering dalam aplikasi, 
di mana low-level modules bertanggung jawab dengan fungsi yang sangat detail dan 
high-level modules menggunakan low-level classes untuk mencapai tugas yang lebih besar. 
Hal ini bisa dicapai dengan bergantung pada sebuah abstraksi, ketika ada ketergantungan 
antar kelas seperti interface, daripada referensi langsung ke kelas lainnya.

Tanpa (DIP)
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

(DIP)
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