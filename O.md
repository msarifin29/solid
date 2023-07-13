O = Open/Close Principle (OCP)

"A software artifact should be open for extension but closed for 
modification." [2] (Bertrand Meyer, 1988)

Sebuah artefak perangkat lunak harus terbuka untuk ditambahkan 
tetapi tertutup untuk dimodifikasi. 

Tanpa (OCP)
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

(OCP)
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
