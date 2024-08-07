import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});


  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(

        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});



  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {


  var wtController = TextEditingController();
  var ftController = TextEditingController();
  var inController = TextEditingController();

  var result = "";
  var bgcolor = Colors.green.shade400;

  @override
  Widget build(BuildContext context) {

    return Scaffold(
      appBar: AppBar(

        title: Text('YourBMI'),
      ),
      body: Container(
        color: bgcolor,
        child: Center(
          child: Container(

            width: 300,
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Text('BMI',style: TextStyle(
                  fontSize: 40, fontWeight: FontWeight.w500
                ),),

                SizedBox(height: 20,),

                TextField(
                  controller: wtController,
                  decoration: InputDecoration(
                    label: Text('Enter Your Weight(in kgs)'),
                    prefixIcon: Icon(Icons.line_weight)
                  ),
                  keyboardType: TextInputType.number,
                ),
                SizedBox(height: 10,),

                  TextField(
                    controller: ftController,
                    decoration: InputDecoration(
                        label: Text('Enter Your Height(in feet)'),
                        prefixIcon: Icon(Icons.height)
                    ),
                    keyboardType: TextInputType.number,
                  ),
                SizedBox(height: 10,),

                  TextField(
                    controller: inController,
                    decoration: InputDecoration(
                        label: Text('Enter Your Height(in inch)'),
                        prefixIcon: Icon(Icons.height)
                    ),
                    keyboardType: TextInputType.number,
                  ),

                SizedBox(height: 15,),

            ElevatedButton(onPressed:(){

              var wt = wtController.text.toString();
              var ft = ftController.text.toString();
              var inch = inController.text.toString();

              if(wt!="" && ft!="" && inch!=""){

                  var iWt = int.parse(wt);
                  var iFt = int.parse(ft);
                  var iInch = int.parse(inch);

                  var tInch = (iFt*12) + iInch;

                  var tcm = tInch*2.54;

                  var tM = tcm/100;

                  var bmi = iWt/(tM*tM);

                  var msg = "";

                  if(bmi>25){
                    msg = "You are over weight!!";
                    bgcolor = Colors.pink;
                  }else if(bmi<18){
                    msg = "You are under weight!!";
                    bgcolor = Colors.purple;

                  }else{
                    msg = "You are healthy!!";
                    bgcolor = Colors.green.shade800;


                  }

                  setState(() {
                    result = "$msg \n Your BMI is: ${bmi.toStringAsFixed(2)}";
                  });


              } else{
                  setState(() {
                    result = "Please fill all the required fields!!";
                  });
              }


            }, child: Text('Calculate')),

                SizedBox(height: 15,),

                Text(result,style: TextStyle(fontSize: 20),)




              ],
            ),
          ),
        ),
      )


      );

  }
}

