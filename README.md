
# Overall Framework Features

## changes in branch 2
# CHanfes in Main Branch
This is a Selenium Hybrid Framework.
- Written in **JAVA**
- Implemented using **TestNG**
- Build Tool - Maven
- Implemented Page Object Model Design Pattern
- Excel TestNG @DataProvider
- WebDriver Manager - Auto Download of required drivers.

### Browsers Supported
- Mozilla Firefox
- Google Chrome
- Opera
- Microsoft Edge Chromium

### Headless Support
- Firefox Headless
- Chrome Headless

### Platform Support
- Windows
- Linux
- Macintosh

---
### Reporting
- [Extent Report](https://www.extentreports.com/docs/versions/4/java/index.html)

Navigate to ./Reports and open the report you want

---

### @DataProviders

**__Method 1:__**
- Use **TestData.xlsx** file as your dataProvider. The Sheet Name should be the name of your Method Name.
- To use a different xlsx file, Create a new `@DataProvider` method and change the workbook name.
```java
@DataProvider(name="multiSheetExcelRead", parallel=true)
public static Object\[][] multiSheetExcelRead(Method method) throws Exception
{
	File file = new File("./src/test/resources/Excel Files/TestData.xlsx");
	String SheetName = method.getName();
	System.out.println(SheetName);
	Object testObjArray\[][] = ExcelUtils.getTableArray(file.getAbsolutePath(), SheetName);
	return testObjArray;
}
```

**__Method 2:__**
- Create Excel Workbook with the same name as your method Name.
```java
@DataProvider(name="excelSheetNameAsMethodName",parallel=true)
public static Object\[][] excelSheetNameAsMethodName(Method method) throws Exception
{
	File file = new File("./src/test/resources/Excel Files/"+method.getName()+".xlsx");
	Object testObjArray\[][] = ExcelUtils.getTableArray(file.getAbsolutePath());
	return testObjArray;
}
 ```
 ---

### @DataProvider Usage

__To Use Method Name as Excel Workbook Name, Use the following:__
```java
@Test(dataProvider="excelSheetNameAsMethodName", dataProviderClass=ExcelDataProvider.class)
```

__To use a Single Workbook with multiple `@DataProvider`sheets, Use:__

~~NOTE~~: SheetName in excel should be the same name as Method Name
```java
@Test(dataProvider="multiSheetExcelRead", dataProviderClass=ExcelDataProvider.class)
```

# Software Required

1. (http://www.seleniumhq.org/) Selenium WebDriver
2. (https://www.java.com/en/download/) Java 8
3. (https://maven.apache.org/download.cgi?Preferred=ftp://ftp.osuosl.org/pub/apache/) Maven


# How to use the Framework

### 1. USING MAVEN
```sh
$ git clone  <https://github.com/TestrigTechnologies/Ribbon_New.git>
```
```sh
$ mvn clean test
```
~~NOTE~~: Check if PR has been merged with the latest branch! Otherwise, clone another branch like Ribbon_Current of the same repository
```
### Browser Setup
- Navigate to *WebAutomation\src\main\resources* change *BrowserType* in the ApplicationConfig.properties or use Maven to invoke different browsers
```
```sh
$ mvn clean test -DBrowserType=Chrome			            #Chrome
$ mvn clean test -DBrowserType=Chrome_Headless		    #Chrome Headless
$ mvn clean test -DBrowserType=Firefox			          #Mozilla Firefox
$ mvn clean test -DBrowserType=Opera			            #Opera Blink
$ mvn clean test -DBrowserType=Edge			              #Microsoft Edge
```

### 2. USING IDE(e.g. Eclipse or IntelliJ IDEA)
		 a. Import your Preferred branch of this repo in Your preferred IDE
		 b. Download all Dependencies using Maven Update
		 c. In the Root folder of the project there are 3 TestNG Suites
				 - Run "TestNG.xml" if you want to run whole Framework
				 - Run "Shoppe.xml" for running the framework for shoppeobject Client
				 - Run "AM.xml" for running the framework for aestheticmovement Client

---
### Report Generation
```sh
$ mvn site
```

### TO-DO
1. Logging
2. File Path
3. Robot class on a non-windows machine
4. Slack integration
5. REST Assured API
