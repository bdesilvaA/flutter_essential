# how to set environment

1. add dependencey
   
```dart
  #environment
  flutter_dotenv: ^5.1.0
```

2. add *dotenv.development* and *dotenv.production* into project index folder

 inside file you can store any key/url/version or anything that deffrent when each envirnments
 
*dotenv.development*
```
FIREBASE_URL=<sample_url>
VERSION=<sample_version>
```

*dotenv.production*
```
FIREBASE_URL=<sample_url>
VERSION=<sample_version>
```

3. define files as assets in pubspec.yaml
   ```yaml
     assets:
    - dotenv.development
    - dotenv.production
   ```

4. add Environment class to haddle the data as the environment
```dart
import 'package:flutter/foundation.dart';
import 'package:flutter_dotenv/flutter_dotenv.dart';

class Environment {

  static String get fileName =>
      kReleaseMode ? "dotenv.production" : "dotenv.development";

  static String get firebaseStorageUrl =>
      dotenv.env['FIREBASE_URL'] ?? 'FALLBACK';

  static String get appVersion => dotenv.env['VERSION'] ?? '1.0.0';
}
```

5. intialize dotenv before runapp() in main function to select the right env file
```dart
Future<void> main() async {
  await dotenv.load(fileName: Environment.fileName);
  runApp(const MyApp());
}
```

6. use variables as you want in the code base
```dart
#example
print(${Environment.firebaseStorageUrl})
print(${Environment.appVersion})
```


