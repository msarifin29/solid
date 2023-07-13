S = Single Responsibility Principle(SRP)

"A module should be responsible to one, and only one, actor." [2] (Robert Cecil Martin, 2017)

setiap class dipisahkan berdasarkan fungsionalitasnya dan hanya akan menangani satu tanggung jawab (fungsi).

Tanpa (SRP)
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
```
 
class Item {}

(SRP)
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