import 'package:flutter/material.dart';
import 'package:myloginapp/authservice.dart';
import 'package:myloginapp/homepage.dart';

class LoginComponent extends StatefulWidget {
  @override
  State<LoginComponent> createState() => _LoginComponentState();
}

class _LoginComponentState extends State<LoginComponent> {
  final _loginformkey = GlobalKey<FormState>();

  final _emailcontroller = TextEditingController();

  final _passcontroller = TextEditingController();

  AuthService service = AuthService();

  bool isVisible = false;

  late String email, pass;

  @override
  Widget build(BuildContext context) {
    return SafeArea(
        child: Scaffold(
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Container(
            height: 100,
            width: 400,
            child: Padding(
                padding: EdgeInsets.all(10),
                child: Text(
                  "FireBase Login",
                  style: TextStyle(
                      color: Colors.teal,
                      fontWeight: FontWeight.bold,
                      fontSize: 40),
                )),
          ),
          SizedBox(
            height: 10,
          ),
          Padding(
            padding: EdgeInsets.symmetric(horizontal: 20),
            child: Container(
              height: 200,
              width: 400,
              child: Form(
                key: _loginformkey,
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.start,
                  children: [
                    TextFormField(
                      controller: _emailcontroller,
                      validator: (value) =>
                          value!.isEmpty ? "Please Enter Valid Email" : null,
                      onSaved: (newValue) => email = newValue!,
                      decoration: InputDecoration(
                          border: OutlineInputBorder(
                              borderRadius: BorderRadius.circular(8)),
                          labelText: "Email"),
                      keyboardType: TextInputType.emailAddress,
                    ),
                    SizedBox(
                      height: 20,
                    ),
                    TextFormField(
                      obscureText: true,
                      controller: _passcontroller,
                      validator: (value) => value!.length <= 8
                          ? "Please Enter Valid Password"
                          : null,
                      onSaved: (newValue) => pass = newValue!,
                      decoration: InputDecoration(
                          border: OutlineInputBorder(
                              borderRadius: BorderRadius.circular(8)),
                          labelText: "Password"),
                      keyboardType: TextInputType.emailAddress,
                    )
                  ],
                ),
              ),
            ),
          ),
          Visibility(
              visible: isVisible,
              child: Text(
                "Wrong Credentials",
                style: TextStyle(color: Colors.red),
              )),
          SizedBox(
            height: 20,
          ),
          Container(
            height: 40,
            width: 200,
            child: ElevatedButton(
              child: Text("Authenticate"),
              onPressed: () async {
                if (_loginformkey.currentState!.validate()) {
                  _loginformkey.currentState!.save();
                  bool? res = await service.authUser(email, pass);
                  if (res == true) {
                    Navigator.of(context).push(
                        MaterialPageRoute(builder: (context) => Homepage()));
                  } else if (res == null) {
                    setState(() {
                      isVisible = true;
                    });
                  }
                }
              },
            ),
          )
        ],
      ),
    ));
  }
}
