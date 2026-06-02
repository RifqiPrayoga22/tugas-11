<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
  <title>Redirecting Constructors • Rifqi Prayoga</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: linear-gradient(145deg, #f9fafc 0%, #f1f5f9 100%);
      font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, Helvetica, sans-serif;
      color: #1e293b;
      line-height: 1.5;
      padding: 2rem 1rem;
    }

    .container {
      max-width: 1280px;
      margin: 0 auto;
      background: rgba(255, 255, 255, 0.6);
      backdrop-filter: blur(2px);
      border-radius: 2rem;
      padding: 2rem 1.5rem;
      box-shadow: 0 20px 35px -12px rgba(0, 0, 0, 0.08), 0 0 0 1px rgba(148, 163, 184, 0.1);
    }

    .header {
      text-align: center;
      margin-bottom: 2.5rem;
      border-bottom: 2px solid #e2e8f0;
      padding-bottom: 1.5rem;
    }

    .header h1 {
      font-size: 2.4rem;
      font-weight: 700;
      background: linear-gradient(135deg, #0f172a, #334155);
      background-clip: text;
      -webkit-background-clip: text;
      color: transparent;
      letter-spacing: -0.02em;
      margin-bottom: 0.5rem;
    }

    .identitas p {
      font-size: 1rem;
      font-weight: 500;
      color: #475569;
      background: #ffffffcc;
      display: inline-block;
      padding: 0.3rem 1.2rem;
      border-radius: 40px;
      backdrop-filter: blur(4px);
      box-shadow: 0 1px 2px rgba(0,0,0,0.02);
    }

    .section {
      margin-bottom: 2.5rem;
      background: #ffffff;
      border-radius: 1.5rem;
      padding: 1.75rem 1.75rem;
      transition: all 0.25s ease;
      border: 1px solid #e9eef3;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.02);
    }

    .section:hover {
      transform: translateY(-3px);
      box-shadow: 0 20px 30px -12px rgba(0, 0, 0, 0.08);
      border-color: #cbd5e1;
    }

    .section h2 {
      font-size: 1.7rem;
      font-weight: 600;
      letter-spacing: -0.01em;
      margin-bottom: 0.5rem;
      color: #0f172a;
      border-left: 5px solid #3b82f6;
      padding-left: 1rem;
    }

    .nama {
      font-size: 0.85rem;
      font-weight: 500;
      color: #4b5563;
      margin-top: 0rem;
      margin-bottom: 1rem;
      display: inline-block;
      background: #f1f5f9;
      padding: 0.2rem 0.9rem;
      border-radius: 20px;
    }

    .section p {
      font-size: 1rem;
      margin-bottom: 1rem;
      color: #2d3a4b;
      line-height: 1.55;
    }

    .section h2::after {
      content: "";
      display: block;
      width: 60px;
      height: 3px;
      background: #3b82f6;
      margin-top: 8px;
      border-radius: 4px;
      transition: width 0.2s;
    }

    .section:hover h2::after {
      width: 100px;
    }

    pre {
      background: #0a0c10 !important;
      color: #ffffff !important;
      padding: 1.25rem;
      border-radius: 1rem;
      overflow-x: auto;
      font-family: 'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace;
      font-size: 0.85rem;
      line-height: 1.5;
      margin: 1rem 0;
      box-shadow: inset 0 0 0 1px rgba(255,255,255,0.08), 0 6px 12px -8px rgba(0,0,0,0.3);
      font-weight: 500;
    }

    pre, pre * {
      color: #ffffff !important;
    }

    .dartpad-embed {
      margin: 1.2rem 0 0.5rem 0;
      border-radius: 1rem;
      overflow: hidden;
      box-shadow: 0 4px 12px rgba(0,0,0,0.08);
      border: 1px solid #e2e8f0;
    }

    iframe {
      width: 100%;
      height: 450px;
      border: none;
      display: block;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin: 1rem 0;
      font-size: 0.9rem;
    }
    th, td {
      border: 1px solid #cbd5e1;
      padding: 0.75rem;
      text-align: left;
      vertical-align: top;
    }
    th {
      background: #f1f5f9;
      font-weight: 600;
    }
    ul {
      margin-left: 1.5rem;
      margin-bottom: 1rem;
    }

    @media (max-width: 680px) {
      body {
        padding: 1rem;
      }
      .container {
        padding: 1rem;
      }
      .header h1 {
        font-size: 1.8rem;
      }
      .section {
        padding: 1.25rem;
      }
      .section h2 {
        font-size: 1.4rem;
      }
      pre {
        font-size: 0.75rem;
        padding: 1rem;
      }
      iframe {
        height: 420px;
      }
      table {
        font-size: 0.75rem;
      }
    }
  </style>
</head>
<body>
<div class="container">
  <div class="header">
    <h1>Redirecting Constructors</h1>
    <div class="identitas">
      <p>Rifqi Prayoga | 251410005 | SI2A</p>
    </div>
  </div>

  <!-- Slide 1: Review Factory Constructors (tanpa DartPad) -->
  <div class="section">
    <h2>1. Review Sesi 10 - Factory Constructors</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Factory constructor: <code>factory class.name()</code>. Bisa return instance yang sudah ada atau subclass. Use cases: singleton, caching, object pools.</p>
    <pre>// Contoh cepat:
factory Shape.circle() => Circle();</pre>
    <!-- Tidak ada DartPad sesuai permintaan -->
  </div>

  <!-- Slide 2: Pengantar Redirecting Constructors (tanpa DartPad) -->
  <div class="section">
    <h2>2. Pengantar Redirecting Constructors</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Apa itu? Constructor yang "mengalihkan" ke constructor lain di kelas yang sama. Tujuan: mengurangi duplikasi kode (DRY principle). Sintaks: <code>: this(...)</code> di initializer list, tidak punya body (tidak ada { }).</p>
    <pre>// Sintaks dasar
class Point {
  Point(this.x, this.y);
  Point.origin() : this(0, 0); // redirecting
  final double x, y;
}</pre>
  </div>

  <!-- Slide 3: Sintaks Dasar - Class Point (dengan DartPad) -->
  <div class="section">
    <h2>3. Sintaks Dasar - Class Point</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Constructor utama menerima x dan y. Constructor pengarah <code>Point.origin()</code>, <code>Point.onXAxis()</code>, dll mengarah ke constructor utama.</p>
    <pre>class Point {
  final double x;
  final double y;
  Point(this.x, this.y);
  Point.origin() : this(0, 0);
  Point.onXAxis(double x) : this(x, 0);
  Point.onYAxis(double y) : this(0, y);
  @override
  String toString() => 'Point($x, $y)';
}

void main() {
  print(Point.origin());
  print(Point.onXAxis(5));
  print(Point.onYAxis(3));
}</pre>
    <div class="dartpad-embed">
      <iframe src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=387ff6c605aa28498495c072ad112a62"></iframe>
    </div>
  </div>

  <!-- Slide 4: Masalah Tanpa Redirecting Constructor (dengan DartPad) -->
  <div class="section">
    <h2>4. Masalah Tanpa Redirecting Constructor</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Tanpa redirecting, kita tidak bisa menginisialisasi field <code>final</code> dari constructor lain, menyebabkan error.</p>
    <pre>class Rectangle {
  final double width;
  final double height;
  Rectangle(this.width, this.height);
  // Tanpa redirecting - duplikasi logika
  // Rectangle.square(double side) {
  //   width = side;  // ERROR: final field
  //   height = side;
  // }
}</pre>
    <div class="dartpad-embed">
      <iframe src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=1e922704418aab425856842ec51640bc"></iframe>
    </div>
  </div>

  <!-- Slide 5: Solusi dengan Redirecting Constructor (dengan DartPad) -->
  <div class="section">
    <h2>5. Solusi: Redirecting Constructor</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Redirecting constructor memanggil constructor utama sehingga field final bisa diinisialisasi dengan benar.</p>
    <pre>class Rectangle {
  final double width;
  final double height;
  Rectangle(this.width, this.height);
  Rectangle.square(double side) : this(side, side);
  Rectangle.widthDefault() : this(100, 50);
  Rectangle.fromWidth(double width) : this(width, width * 0.618);
  @override
  String toString() => 'Rectangle(w:${width.toStringAsFixed(2)}, h:${height.toStringAsFixed(2)})';
}

void main() {
  print(Rectangle.square(10));
  print(Rectangle.widthDefault());
  print(Rectangle.fromWidth(100));
}</pre>
    <div class="dartpad-embed">
      <iframe src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=adfdd9cbf93e04f4da750553b80a09e4"></iframe>
    </div>
  </div>

  <!-- Slide 6: Redirecting dengan Named Parameters (dengan DartPad) -->
  <div class="section">
    <h2>6. Redirecting dengan Named Parameters</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Constructor utama menggunakan named parameters, redirecting constructor memberikan nilai default.</p>
    <pre>class Person {
  final String name;
  final int age;
  final String? email;
  Person({required this.name, required this.age, this.email});
  Person.anonymous() : this(name: 'Anonymous', age: 0);
  Person.fromName(String name) : this(name: name, age: 0);
  Person.adult(String name) : this(name: name, age: 18);
  Person.child(String name, int years) : this(name: name, age: years, email: null);
  @override
  String toString() => 'Name: $name, Age: $age, Email: ${email ?? "N/A"}';
}

void main() {
  print(Person.anonymous());
  print(Person.fromName('Alice'));
  print(Person.adult('Bob'));
  print(Person.child('Charlie', 10));
}</pre>
    <div class="dartpad-embed">
      <iframe src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=52da765147822448262e183230df2029"></iframe>
    </div>
  </div>

  <!-- Slide 7: Praktik 1 - Configuration Class (dengan DartPad) -->
  <div class="section">
    <h2>7. Praktik 1 - Configuration Class</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Membuat class konfigurasi dengan redirecting constructor untuk berbagai environment.</p>
    <pre>class AppConfig {
  final String environment;
  final String apiUrl;
  final bool debugMode;
  AppConfig({required this.environment, required this.apiUrl, required this.debugMode});
  AppConfig.development() : this(environment: 'development', apiUrl: 'http://localhost:3000', debugMode: true);
  AppConfig.production() : this(environment: 'production', apiUrl: 'https://api.example.com', debugMode: false);
  AppConfig.staging() : this(environment: 'staging', apiUrl: 'https://staging.example.com', debugMode: true);
  void printConfig() {
    print('Environment: $environment');
    print('API URL: $apiUrl');
    print('Debug Mode: $debugMode');
    print('---');
  }
}

void main() {
  AppConfig.development().printConfig();
  AppConfig.production().printConfig();
  AppConfig.staging().printConfig();
}</pre>
    <div class="dartpad-embed">
      <iframe src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=9001d123fb58fba0ab3b80d216aadf16"></iframe>
    </div>
  </div>

  <!-- Slide 8: Redirecting dengan Validasi (dengan DartPad) -->
  <div class="section">
    <h2>8. Redirecting dengan Validasi</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Validasi dilakukan di constructor utama, redirecting constructor hanya mengarahkan.</p>
    <pre>class Temperature {
  final double celsius;
  Temperature(this.celsius) {
    if (celsius < -273.15) throw ArgumentError('Suhu tidak boleh di bawah absolute zero');
  }
  Temperature.fahrenheit(double f) : this((f - 32) * 5 / 9);
  Temperature.kelvin(double k) : this(k - 273.15);
  Temperature.roomTemp() : this(22);
  @override String toString() => '${celsius.toStringAsFixed(1)}°C';
}

void main() {
  print(Temperature.roomTemp());
  print(Temperature.fahrenheit(98.6));
  print(Temperature.kelvin(300));
  try { Temperature(-300); } catch(e) { print('Error: $e'); }
}</pre>
    <div class="dartpad-embed">
      <iframe src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=6cecb27d20b0a8ac74f0f3660934e3b2"></iframe>
    </div>
  </div>

  <!-- Slide 9: Multiple Redirecting Levels (dengan DartPad) -->
  <div class="section">
    <h2>9. Multiple Redirecting Levels</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Redirecting constructor bisa berantai, semua akhirnya ke constructor utama.</p>
    <pre>class Product {
  final String id;
  final String name;
  final double price;
  final String category;
  final int stock;
  final DateTime? expiryDate;
  Product({required this.id, required this.name, required this.price, required this.category, required this.stock, this.expiryDate});
  Product.basic(String id, String name, double price) : this(id: id, name: name, price: price, category: 'General', stock: 0);
  Product.withCategory(String id, String name, double price, String category) : this(id: id, name: name, price: price, category: category, stock: 0);
  Product.full({required String id, required String name, required double price, required String category, required int stock, DateTime? expiry}) 
      : this(id: id, name: name, price: price, category: category, stock: stock, expiryDate: expiry);
  @override String toString() => 'Product($id, $name, \$$price, $category, stock: $stock)';
}

void main() {
  print(Product.basic('P001', 'Item 1', 10));
  print(Product.withCategory('P002', 'Item 2', 20, 'Electronics'));
  print(Product.full(id: 'P003', name: 'Item 3', price: 30, category: 'Food', stock: 100));
}</pre>
    <div class="dartpad-embed">
      <iframe src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=f8a861cc929a321f19cc6202ab206f37"></iframe>
    </div>
  </div>

  <!-- Slide 10: Redirecting vs Factory Constructor (tabel, tanpa DartPad) -->
  <div class="section">
    <h2>10. Redirecting Constructor vs Factory Constructor</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p>Perbandingan perbedaan utama.</p>
    <table>
      <thead><tr><th>Aspect</th><th>Redirecting Constructor</th><th>Factory Constructor</th></tr></thead>
      <tbody>
        <tr><td>Tujuan</td><td>Panggil constructor lain di class yang sama</td><td>Logika kompleks, caching, subclass</td></tr>
        <tr><td>Return</td><td>Harus instance class ini</td><td>Bisa instance yang sudah ada atau subclass</td></tr>
        <tr><td>Body</td><td>Tidak ada (hanya : this(...))</td><td>Ada body bisa berisi logika</td></tr>
        <tr><td>Final fields</td><td>Bisa diinisialisasi</td><td>Tidak bisa (harus lewat constructor lain)</td></tr>
        <tr><td>Use case</td><td>Default parameters, convenience</td><td>Singleton, object pool, polymorphism</td></tr>
      </tbody>
    </table>
    <!-- Tidak ada DartPad sesuai permintaan -->
  </div>

  <!-- Slide 11: Tips & Best Practices (dengan DartPad opsional, tapi tidak masalah) -->
  <div class="section">
    <h2>11. Tips &amp; Best Practices</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <ul>
      <li><strong>Gunakan redirecting constructor untuk:</strong> default parameter values, convenience constructors, alternative ways to create objects.</li>
      <li><strong>Hindari untuk:</strong> complex logic (gunakan factory), caching (gunakan factory), subclass creation (gunakan factory).</li>
      <li><strong>Tips:</strong> Keep redirecting chains short, document the purpose of each constructor, use meaningful names.</li>
    </ul>
    <!-- Tidak perlu DartPad, tapi boleh tetap tidak masalah. Saya akan hilangkan. -->
  </div>

  <!-- Slide 12: Ringkasan & Latihan (dengan DartPad) -->
  <div class="section">
    <h2>12. Ringkasan &amp; Latihan</h2>
    <div class="nama">Rifqi Prayoga 251410005 SI2A</div>
    <p><strong>Ringkasan:</strong></p>
    <ul>
      <li>Redirecting constructor: <code>: this(...)</code> tanpa body</li>
      <li>Untuk memanggil constructor lain di class yang sama → mengurangi duplikasi kode</li>
      <li>Tidak bisa berisi logic kompleks</li>
    </ul>
    <p><strong>Latihan:</strong> Buat class <code>Circle</code> dengan:</p>
    <ul>
      <li>Main constructor dengan <code>radius</code></li>
      <li>Redirecting constructor dari <code>diameter</code></li>
      <li>Redirecting constructor dari <code>keliling</code> (2 * pi * r)</li>
      <li>Redirecting constructor dari <code>luas</code> (pi * r^2)</li>
    </ul>
    <pre>// Contoh solusi latihan
import 'dart:math';
class Circle {
  final double radius;
  Circle(this.radius);
  Circle.fromDiameter(double d) : this(d / 2);
  Circle.fromCircumference(double c) : this(c / (2 * pi));
  Circle.fromArea(double a) : this(sqrt(a / pi));
  @override String toString() => 'Circle(r=${radius.toStringAsFixed(2)})';
}
void main() {
  print(Circle.fromDiameter(10));
  print(Circle.fromCircumference(31.4159));
  print(Circle.fromArea(78.5398));
}</pre>
    <div class="dartpad-embed">
      <iframe src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=edfd349f4a37a6e6d426f6eafeb1ef35"></iframe>
    </div>
  </div>
</div>
</body>
</html>
