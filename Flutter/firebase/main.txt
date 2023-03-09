import 'package:firebase_core/firebase_core.dart';
import 'package:flutter/material.dart';
import 'package:myloginapp/myapp.dart';

void main() async {
  try {
    WidgetsFlutterBinding.ensureInitialized();
    await Firebase.initializeApp(
        options: FirebaseOptions(
            apiKey: "AIzaSyBYQBI__aHxQxYcJ1ijcFY8IMZKvPUQr1Q",
            appId: "1:269709872177:android:4031b489fc1eb700a69910",
            messagingSenderId: "269709872177",
            projectId: "myloginapp-cf218"));
    runApp(const MyApp());
  } on Exception catch (e) {
    // TODO
    print(e);
  }
}
