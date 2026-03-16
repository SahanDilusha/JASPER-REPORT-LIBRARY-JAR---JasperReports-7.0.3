# JasperReports 7.0.3 Library Bundle

This repository/folder contains the required `.jar` library files to run **JasperReports 7.0.3** successfully within **Apache NetBeans 28** using **Java JDK 25**. 

This specific bundle has been curated to include the core engine, PDF generation capabilities (via OpenPDF), barcode generation, JSON/XML data parsing, and MySQL database connectivity.

## 🛠️ Environment Requirements

*   **Java Development Kit (JDK):** Version 25
*   **IDE:** Apache NetBeans 28
*   **JasperReports Engine:** Version 7.0.3

## 📦 Included Libraries (JAR Files)

The following libraries are included in this package. They are categorized by their functionality to help you understand their purpose in your application:

### 1. JasperReports Core & Compilers
*   `jasperreports-7.0.3.jar` - The core JasperReports library.
*   `jasperreports-jdt-7.0.3.jar` - Java compiler integration for compiling report expressions.
*   `ecj-4.3.1.jar` - Eclipse Compiler for Java (Required for compiling `.jrxml` files at runtime).

### 2. PDF Export Capabilities
*(Note: JasperReports 7.x utilizes OpenPDF instead of the older iText library)*
*   `jasperreports-pdf-7.0.3.jar` - JasperReports PDF exporter extension.
*   `openpdf-1.3.30.jar` - The underlying PDF generation library.

### 3. Barcode Support
*   `barbecue-1.5-beta1.jar` - Core Barbecue library for generating barcodes.
*   `jasperreports-barbecue-7.0.3.jar` - Integration bridge between JasperReports and Barbecue.

### 4. JSON & XML Data Processing
*   `jackson-core-2.15.2.jar` - Core JSON processor.
*   `jackson-databind-2.15.2.jar` - Data-binding for JSON.
*   `jackson-annotations-2.15.2.jar` - Annotations for Jackson.
*   `jackson-dataformat-xml-2.15.2.jar` - XML data format module for Jackson.
*   `woodstox-core-6.5.1.jar` - High-performance XML processor.
*   `stax2-api-4.2.1.jar` - XML Streaming API extension.

### 5. Apache Commons (Utility Dependencies)
*   `commons-beanutils-1.9.4.jar` - Utility methods for populating JavaBeans.
*   `commons-collections4-4.4.jar` - Extended Java Collections framework.
*   `commons-digester-2.1.jar` - XML-to-Java-object mapping utility.
*   `commons-logging-1.2.jar` - Bridge for logging frameworks.

### 6. Database Connectivity
*   `mysql-connector-j-9.5.0.jar` - Official MySQL JDBC Driver to connect your reports to a MySQL database.

### 7. User Interface (Optional Viewer Theme)
*   `flatlaf-3.5.4.jar` - Flat Look and Feel (Used if you are building a modern Swing-based JasperViewer).

---

## ⚙️ How to Add to NetBeans 28

If you are using a standard Ant-based Java project in NetBeans, follow these steps to add the libraries:

1. Open your project in **NetBeans 28**.
2. In the **Projects** window on the left, right-click on the **Libraries** folder.
3. Select **Add JAR/Folder...**
4. Navigate to the folder where you saved these JAR files.
5. Highlight **all** the `.jar` files listed above and click **Open**.
6. Expand the Libraries folder to verify they have been added successfully.

---

## 🚀 Quick Start Example Code

Here is a quick example of how to compile a `.jrxml` file, fill it with a MySQL database connection, and export it to a PDF using JDK 25:

```java
import net.sf.jasperreports.engine.*;
import java.sql.Connection;
import java.sql.DriverManager;
import java.util.HashMap;

public class ReportGenerator {
    
    public static void main(String[] args) {
        try {
            // 1. Connect to MySQL Database
            Connection conn = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/your_database", "username", "password"
            );

            // 2. Compile the JRXML file into a JasperReport object
            JasperReport jasperReport = JasperCompileManager.compileReport("src/reports/MyReport.jrxml");

            // 3. Fill the report with data
            HashMap<String, Object> parameters = new HashMap<>();
            parameters.put("ReportTitle", "Monthly Sales Report");
            
            JasperPrint jasperPrint = JasperFillManager.fillReport(jasperReport, parameters, conn);

            // 4. Export the filled report to a PDF file
            JasperExportManager.exportReportToPdfFile(jasperPrint, "OutputReport.pdf");
            
            System.out.println("Report successfully generated!");
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
