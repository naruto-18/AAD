import 'package:firebase_auth/firebase_auth.dart';

class AuthService {
  FirebaseAuth _auth = FirebaseAuth.instance;

  Future authUser(String email, String pass) async {
    try {
      User? result =
          (await _auth.signInWithEmailAndPassword(email: email, password: pass))
              .user;

      if (result != null) {
        return true;
      }
    } catch (e) {
      print(e);
    }
  }
}
