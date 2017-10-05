# Arduino_Rain-Gauge
 Arduino sketch to record the switching of the reed switch in the rain gauge


What is it?
A rain gauge is an instrument you can use to measure the amount of rainfall your area receives in a given time period.
How to connect Rain Gauge to arduino?
The ends of the reed switch are connected to Ground and Digital Pin 9.


Source code :




/*

Arduino sketch to record the switching of the reed switch in the rain gauge

The sketch works by counting the number of times the reed switch changes status (HIGH or LOW)

*/


const int REED = 9;                             //The reed switch outputs to digital pin 9

int val = 0;                                    //Current value of reed switch

int old_val = 0;                                //Old value of reed switch

int REEDCOUNT = 0;                              //This is the variable that hold the count of switching

float volume_of_rain;
float area_of_funnel;
float depth_of_rain;

void setup(){

 Serial.begin(9600);

 pinMode (REED, INPUT_PULLUP);                   //This activates the internal pull up resistor

}


void loop(){

 val = digitalRead(REED);                         //Read the status of the Reed swtich


 if ((val == LOW) && (old_val == HIGH)){          //Check to see if the status has changed

   delay(10);                                     // Delay put in to deal with any "bouncing" in the switch.

   REEDCOUNT = REEDCOUNT + 1;                     //Add 1 to the count of bucket tips

   old_val = val;                                 //Make the old value equal to the current value

volume_of_rain = (5.94*REEDCOUNT)/1000;        //volume of rain that fell 

area_of_funnel = (3.14/4)*0.165*0.165;         //area of the funnel

depth_of_rain = volume_of_rain/area_of_funnel; //depth of rain

 Serial.print("Count = ");

Serial.println(REEDCOUNT);                     //Output the count to the serial monitor
Serial.print("rain = ");

Serial.print(depth_of_rain);                  //Output of depth_of_rain
Serial.println(" mm ");


 }


 else {

   old_val = val;                                //If the status hasn't changed then do nothing

 }

}


