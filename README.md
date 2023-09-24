# flutter-database-helper
An integration of a sql database that works for flutter projects which uses a general implementation of the package `sqflite`.
It uses also two other packages to help provide the application string to the app's folder.
Here I have used a custom Object called Water, from one of my projects to demonstrate how to use such an object with the database.
More on the dependencies in [dependencies]

## How to use it
1. Download the DatabaseHelper.dart file;
2. Place it in your project's lib folder;
3. Add ```WidgetsFlutterBinding.ensureInitialized();``` inside the main method of your app;
4. Call an instance of it wherever you want to use it.

### Adding an object into the database
```dart
  Water w = new Water(
    waterDrunk: 1000,
    dailyWater: 2500,
    date: DateTime.now().toString()
  );  
  // The id will be autogenerated
  // Adds the object into a specific table in the database
  DatabaseHelper.instance.AddWater(w);
```
It's possible to also create a general method that takes an argument for the table you want to put the object in.

### Getting a list of objects
```dart
  // Using the object inserted in the code above
  List<Water> list = await DatabaseHelper.instance.GetTable();
  for(var v in list) print(v.waterDrunk); // 1000
```
Note how the await keyword is **required** because we are calling an external tool that comunicates with a database: this is telling the compiler to wait for a response from the database itself.

### Update an object
```dart
  int id = 0;
  Water w = new Water(
    id: id,
    waterDrunk: 1500,
    dailyWater: 2500,
    date: DateTime.now().toString
  );

  DatabaseHelper.instance.UpdateWater(w, id); // New value for waterDrunk = 1500;
```

### Remove an object
```dart
  int id = 0;
  DatabaseHelper.instance.RemoveWater(id); // Removes the object with id = 0;
```

### Remove a table
```dart
  DatabaseHelper.instance.DeleteTable("water");
```
  
##  Dependencies 
This project uses some external packages to work.
External packages used:
1. [sqflite]
2. [path_provider]

Install them from [pub.dev] or just use:
  ```terminal
  $ flutter pub add sqflite
  $ flutter pub add path_provider
  ```
[dependencies]: https://github.com/SirioRigel/flutter-databse-helper/tree/testBranch#dependencies
[sqflite]: https://pub.dev/packages/sqflite
[path_provider]: https://pub.dev/packages/path_provider
[pub.dev]: https://pub.dev
