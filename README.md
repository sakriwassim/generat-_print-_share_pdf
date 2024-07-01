# Flutter PDF Generator, Printer, and Sharer

This project is a Flutter application that demonstrates how to generate, print, and share a PDF document. The application uses the `pdf` and `printing` packages to create and handle PDF documents.

## Features

- Generate a PDF document with custom content.
- Print the generated PDF document.
- Share the generated PDF document.

## Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/sakriwassim/generat-_print-_share_pdf.git
   cd flutter-pdf-app
   ```

2. **Install dependencies:**

   ```bash
   flutter pub get
   ```

3. **Run the application:**

   ```bash
   flutter run
   ```

## Code Overview

### Main Entry Point

The main entry point of the application is the `main.dart` file. It initializes the Flutter application and sets up the `MyApp` widget.

```dart
import 'package:flutter/material.dart';
import 'package:pdf/pdf.dart';
import 'package:pdf/widgets.dart' as pw;
import 'package:printing/printing.dart';

void main() {
  runApp(MyApp());
}
```

### MyApp Widget

The `MyApp` widget is a stateless widget that sets up the application with a title and a theme. It defines the `MyHomePage` widget as the home screen.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Generate, Print, Share PDF',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}
```

### MyHomePage Widget

The `MyHomePage` widget is a stateless widget that creates and manages the PDF document. It defines methods for printing and sharing the PDF.

```dart
class MyHomePage extends StatelessWidget {
  final pdf = pw.Document();

  MyHomePage() {
    pdf.addPage(
      pw.Page(
        build: (pw.Context context) => pw.Center(
          child: pw.Text('Hello, World! Wassim Sakri, sakriwassim@gmail.com'),
        ),
      ),
    );
  }

  void _printDocument() {
    Printing.layoutPdf(
      onLayout: (PdfPageFormat format) async => pdf.save(),
    );
  }

  void _shareDocument() async {
    final pdfBytes = await pdf.save();
    await Printing.sharePdf(
      bytes: pdfBytes,
      filename: 'document.pdf',
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Flutter Demo Home Page'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            ElevatedButton(
              onPressed: _printDocument,
              child: Text('Print'),
            ),
            ElevatedButton(
              onPressed: _shareDocument,
              child: Text('Share'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Usage

1. **Print the PDF:**
   - Tap the "Print" button to print the generated PDF document.

2. **Share the PDF:**
   - Tap the "Share" button to share the generated PDF document.

## Dependencies

- `flutter`: The Flutter framework.
- `pdf`: A library for creating PDF documents.
- `printing`: A library for printing and sharing PDF documents.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
