# dart_freezed_package_discovery
Try to figure out the best of the freezed package and add some comments and explanations

## Prerequisites
Let's define the notion of factory constructor that will be used along with the `freezed` package:

`factory:` A factory constructor is generally used to control the instance creation.

## To add in pubspec.yaml
```yaml
dependencies:
  freezed_annotation: any

dev_dependencies:
  builder_runner: any
  freezed: any
  json_serializable: any
```

`freezed_annotation: any` will provide the `@Freezed` annotation

`builder_runner: any` will also us to launch a command to generate the freezed code

`freezed: any` will provide the `freezed` functionalities

`json_serializable: any` will provide the the ability to serialize/deserialize the classes

## Turn a dart class into a freezed class

### Automatically generated methods
Here is a list of methods that the **freezed** package can generate with just some annotations:
- `copyWith` method
- `toString` method
- `fromJson` method
- `toJson` method
- `equality` operator override

`copyWith` and `toString` between classes instances are methods that can transform a simple `dart class` into a `data class`.

A `data class` is `immutable` and has `copyWith` and `toString` methods and overrides the equality operator.

For serialization, defining only the `fromJson` method in the class is enough, the `toJson` method will be generated automatically. 

### Boilerplate code example
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'my_freezed_class.freezed.dart';
part 'my_freezed_class.g.dart';

@freezed
abstract class User with _$User {
  const factory User({
    String name,
    String email,
  }) = _User;

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
}
```

Once the boilerplate is written, you can run the following command in order to generate the code:
```shell
flutter pub run build_runner build --delete-conflicting-outputs
```

## Support Sealed Unions
With the freezed package, you can also do _Sealed Unions / Pattern matching_

### Nested Sealed classes

### Non-nested Sealed classes

