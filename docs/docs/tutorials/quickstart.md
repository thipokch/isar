---
title: Quickstart
---

# Quickstart

Holy smokes you're here! Let's get started on using the coolest Flutter database out there...

We're going to be short on words and quick on code in this quickstart.

## 1. Add dependencies

First, add Isar to your project. Add the following packages to your `pubspec.yaml`. Always use the latest version.

```yaml
isar_version: &isar_version 3.0.0 # define the version to be used

dependencies:
  isar: *isar_version
  isar_flutter_libs: *isar_version # contains Isar Core

dev_dependencies:
  isar_generator: *isar_version
  build_runner: any
```

## 2. Annotate classes

Annotate your classes with `@collection` and choose an `Id` field.

```dart
part 'email.g.dart';

@collection
class User {
  Id id = Isar.autoIncrement; // you can also use id = null to auto increment

  String? name;

  int? age;
}
```

## 3. Run code generator

Execute the following command to start the `build_runner`:

```
dart run build_runner build
```

If you are using Flutter, use:

```
flutter pub run build_runner build
```

## 4. Open Isar instance

Open a new Isar instance and pass all of your collection schemas. Optionally you can specify an instance name and directory.

```dart
final isar = await Isar.open([EmailSchema]);
```

## 5. Write and read

Once your instance is open, you can start using the collections.

All basic CRUD operations are available via the `IsarCollection`.

```dart
final newUser = User()..name = 'Jane Doe'..age = 36;

await isar.writeTxn(() async {
  await isar.users.put(newUser); // insert & update
});

final existingUser = await isar.users.get(newUser.id); // get

await isar.writeTxn(() async {
  await isar.users.delete(existingUser.id!); // delete
});
```

## Other resources

You're a visual learner? Check out these videos to get started with Isar:
<div class="video-block">
  <iframe max-width=100% height=auto src="https://www.youtube.com/embed/CwC9-a9hJv4" title="Isar Database" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>
<div class="video-block">
  <iframe max-width=100% height=auto src="https://www.youtube.com/embed/videoseries?list=PLKKf8l1ne4_hMBtRykh9GCC4MMyteUTyf" title="Isar Database" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>
<div class="video-block">
  <iframe max-width=100% height=auto src="https://www.youtube.com/embed/pdKb8HLCXOA " title="Isar Database" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
