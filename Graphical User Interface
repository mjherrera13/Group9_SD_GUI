# LSU Biological Engineering - Group 9 Senior Design - Graphical User Interface
This is the code written for the graphical user interface. The code was written in Processing and designed specifically for the scope of Senior Design.

import com.dhchoi.*;
import com.dhchoi.CountdownTimerService;


import controlP5.*;

import ddf.minim.*;
import ddf.minim.analysis.*;
import ddf.minim.effects.*;
import ddf.minim.signals.*;
import ddf.minim.spi.*;
import ddf.minim.ugens.*;

import processing.serial.*;

CountdownTimer timer;
String timerCallbackInfo = " ";
String timertext = "Insert time duration:";
String time;



float floatnumbertimer;
long longnumbertimer;
long adjustedtimer = 10000;
//float inputtime;

Serial myPort;  // Create object from Serial class
String imu = null;     // Data received from the serial port
PFont myFont;

PrintWriter output;

ControlP5 cp5;
String text;
String sensitivity;
float numbertext;
float numbersensitivity;

float adjustedroll;

float scaledinput;
float scaledinput2;
float scaledroll2;
float scaledroll;
float scaledtimer;
float scaledpitch2;
float adjustedpitch;


Minim minim;

AudioSample buzzer2;
AudioSample buzzer1;

//AudioPlayer number0;
//AudioPlayer number1;
//AudioPlayer number2;
//AudioPlayer number3;
//AudioPlayer number4;
//AudioPlayer number5;
//AudioPlayer number6;
//AudioPlayer number7;
//AudioPlayer number8;
//AudioPlayer number9;
//AudioPlayer number10;


int StableXOn, StableYOn;      // Position of stable function start button
int StableXOff, StableYOff;      // Position of stable function stop button   


int StableSize = 25;     // Diameter 

color baseColor;  // colors of buttons when clicked, not clicked
color StableNeutralColor;

color StableHighlight;
color CurrentColor1, CurrentColor2, CurrentColor3, CurrentColor4, OnColor, OffColor, NeutralColor, timercolor;

boolean StableOverOn = false;    
boolean StableOverOff = false;


// width = 1200
// height = 700


void setup()
{
  size(1200, 700);
  myFont = createFont("Arial",16,true);
  textFont(myFont, 18);
  // I know that the first port in the serial list on my mac
  // is Serial.list()[0].
  // On Windows machines, this generally opens COM1.
  // Open whatever port is the one you're using.
  String portName = Serial.list()[0]; //change the 0 to a 1 or 2 etc. to match your port
  myPort = new Serial(this, portName, 115200);
  myPort.bufferUntil('\n');
  
  minim = new Minim(this);

  // load BD.wav from the data folder
  //number0 = minim.loadFile( "0.wav", // filename
  //                          2000      // buffer size
  //                       );
                         
  //number1 = minim.loadFile("1.wav", 2000);
  //number2 = minim.loadFile("2.wav", 2000);
  //number3 = minim.loadFile("3.wav", 2000);
  //number4 = minim.loadFile("4.wav", 2000);
  //number5 = minim.loadFile("5.wav", 2000);
  //number6 = minim.loadFile("6.wav", 2000);
  //number7 = minim.loadFile("7.wav", 2000);
  //number8 = minim.loadFile("8.wav", 2000);
  //number9 = minim.loadFile("9.wav", 2000);
  //number10 = minim.loadFile("10.wav", 2000);
  
  buzzer2 = minim.loadSample("beep-08b.mp3", 2000); 
  //buzzer1 = minim.loadSample("Basketball Buzzer-SoundBible.com-1863250611.mp3", 10000);
    
  // if a file doesn't exist, loadSample will return null
  // if ( number1 == null ) println("Didn't get sound1!");
  
   
  // if ( number2 == null ) println("Didn't get sound2!"); // 
  
  
  cp5 = new ControlP5(this);
  
  cp5.addBang("Angle").setPosition(250,200).setSize(100,40).getCaptionLabel().align(ControlP5.CENTER, ControlP5.CENTER).setFont(myFont);
  cp5.addTextfield("setangle").setPosition(150, 200).setSize(100,40).setFont(myFont).setFocus(true).setColor(color(255)).setAutoClear(false).setColorValue(color(0)).setColorActive(color(0,0,255)).setColorBackground(color(255));
  
  cp5.addBang("Start").setPosition(340,600).setSize(100,40).getCaptionLabel().align(ControlP5.CENTER, ControlP5.CENTER).setFont(myFont);
  cp5.addBang("Reset").setPosition(440,600).setSize(100,40).getCaptionLabel().align(ControlP5.CENTER, ControlP5.CENTER).setFont(myFont);
  cp5.addTextfield("timing").setPosition(240, 600).setSize(100,40).setFont(myFont).setFocus(true).setColor(color(255)).setAutoClear(false).setColorValue(color(0)).setColorActive(color(0,0,255)).setColorBackground(color(255));
  
  cp5.addBang("Number").setPosition(250,400).setSize(100,40).getCaptionLabel().align(ControlP5.CENTER, ControlP5.CENTER).setFont(myFont);
  cp5.addTextfield("Sensitive").setPosition(150, 400).setSize(100,40).setFont(myFont).setFocus(true).setColor(color(255)).setAutoClear(false).setColorValue(color(0)).setColorActive(color(0,0,255)).setColorBackground(color(255));
  
  
  StableXOn = (width/2) - (220);               // locations of buttons for each program on/off
  StableYOn = (height/2) - (StableSize*13);
  StableXOff = (width/2) - (170);               // locations of buttons for each program on/off
  StableYOff = (height/2) - (StableSize*13);   
  
  StableHighlight = color(167);
  
  OnColor = color(0, 255, 0);
  OffColor = color(255, 0, 0);
  NeutralColor = color(255);
  CurrentColor3 = color(255); // Color3 = on switch 
  CurrentColor4 = color(255, 0, 0);
  
  // timer
 
  timer = CountdownTimerService.getNewCountdownTimer(this);

    
  
}

void draw()
{
  background(255);
  float[] euler = null;
  euler = float(split(imu, ","));
  float roll = euler[0];
  float pitch = euler[1];
  float roll2;
  strokeWeight(4);
  fill(0);
  
  // draw timer
  
  text(timertext, width/2 - 575, height/2 + 270);
  text(timerCallbackInfo, width/2 - 575, height/2 + 295);
  
   
  
  strokeWeight(4);  
  update(mouseX, mouseY);
  textFont(myFont, 20);
  text("On", StableXOn + 15, StableYOn + 45);
  text("Off", StableXOn + 64, StableYOn + 45);
  text("Click for sound", StableXOn - 15, StableYOn - 10);
  textFont(myFont, 30);
  text("BarGraph Function", 25, 30);
  line(25, 40, 275, 40);
  textFont(myFont, 18);
  text("Roll: " + adjustedroll, 1000, 80);
  text("Pitch: " + pitch, 1000, 120);
  
  line(100, 135, 400, 135); // text above angle button
  line(100, 270, 400, 270);
  line(100, 135, 100, 270);
  line(400, 135, 400, 270);
  text("Pick an angle value between 0-180,", 110, 160);
  text("then click the ANGLE button", 140, 180);
  
  line(100, 335, 400, 335); //text above sensitivity button
  line(100, 470, 400, 470);
  line(100, 335, 100, 470);
  line(400, 335, 400, 470);
  text("Pick a number between 1-10,", 110, 360);
  text("then click the NUMBER button", 110, 380);
  
  line(20, 520, 550, 520); //text above timer button
  line(20, 670, 550, 670);
  line(20, 520, 20, 670);
  line(550, 520, 550, 670);
  text("Input time for timer (in seconds). Data will be recorded", 60, 540);
  text("during this time period. Click the START button to start", 60, 560);
  text("the timer and the RESET button to reset the timer.", 60, 580);

  
  //adjust incoming values of roll
  
  if (roll > -180 && roll < -90)
  {
    adjustedroll = roll + 270;
  }
  else if (roll > 90 && roll < 180)
  {
    adjustedroll = roll - 90;
  }


  
  // draw heading reference 
  
  line(1080, 480, 1080, 680);
  line(980, 580, 1180, 580);
  stroke(255, 0, 0);
  float scaledadjustedroll = map(adjustedroll, 0, 180, 200, 0);
  line(980 + scaledadjustedroll, 570, 980 + scaledadjustedroll, 590);
  
  float scaledpitch = map(pitch, -90, 90, 0, 200);
  line(1070, 480 + scaledpitch, 1090, 480 + scaledpitch);
  
  
  
  //if (pitch < -90)
  //{
  //  line(300, 445, 300, 455);
  //}
  
  //if (roll < 0 && roll > -90)
  //{
  //  line(290, 270, 310, 270);
  //}
  
  //if (roll > 0 && roll < 90)
  //{
  //  line(290, 630, 310, 630);
  //}
  
  stroke(0);
  
  
  // highlight on/off buttons 
  
  if (StableOverOn) // if mouse is over stable on, highlight
  {
    fill(StableHighlight);
    stroke(0);
    rect(StableXOn, StableYOn, StableSize*2, StableSize);
    fill(0);    
  } 
  else   // if mouse isn't over stable on, leave white 
  {
    fill(CurrentColor3);
    stroke(0);
    rect(StableXOn, StableYOn, StableSize*2, StableSize);
    fill(0);
  }  
  
  if (StableOverOff)   // if mouse over stable off button, highlight 
  {
    fill(StableHighlight);
    stroke(0);
    rect(StableXOff, StableYOff, StableSize*2, StableSize);
    fill(0);
  } 
  else 
  {
    fill(CurrentColor4);
    stroke(0);
    rect(StableXOff, StableYOff, StableSize*2, StableSize);
    fill(0);
  }
    
  

  //draw bar graph with blocks
  
  line(560, 700, 560, 0);
  line(640, 700, 640, 0);
  line(560, 700, 640, 700);
  line(560, 0, 640, 0);
  text("1", 600, 665);
  text("2", 600, 595);
  text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);
 
  
  //draw degree scale on bar graph 
  
  fill(0);
  
  text("20", 755, height - (height/9) + 7);
  text("20", 905, height - (height/9) + 7);
  text("40", 755, height - (2*height/9) + 7);
  text("40", 905, height - (2*height/9) + 7);
  text("60", 755, height - (3*height/9) + 7);
  text("60", 905, height - (3*height/9) + 7);
  text("80", 755, height - (4*height/9) + 7);
  text("80", 905, height - (4*height/9) + 7);
  text("100", 747, height - (5*height/9) + 7);
  text("100", 905, height - (5*height/9) + 7);
  text("120", 747, height - (6*height/9) + 7);
  text("120", 905, height - (6*height/9) + 7);
  text("140", 747, height - (7*height/9) + 7);
  text("140", 905, height - (7*height/9) + 7);
  text("160", 747, height - (8*height/9) + 7);
  text("160", 905, height - (8*height/9) + 7);
  text("180", 747, height - (8.9*height/9) + 7);
  text("180", 905, height - (8.9*height/9) + 7);
 
  
  strokeWeight(2);
  line(780, height - (height/9), 800, height - (height/9)); //line at 20 degrees 
  line(880, height - (height/9), 900, height - (height/9));
  line(790, height - (height/18), 800, height - (height/18)); 
  line(880, height - (height/18), 890, height - (height/18));
  
  line(780, height - (2*height/9), 800, height - (2*height/9)); //line at 40 degrees
  line(880, height - (2*height/9), 900, height - (2*height/9));
  line(790, (height - (height/18)) - (height-(2*height/9)), 800, (height - (height/18)) - (height-(2*height/9)));
  line(880, (height - (height/18)) - (height-(2*height/9)), 890, (height - (height/18)) - (height-(2*height/9)));
  
  line(780, height - (3*height/9), 800, height - (3*height/9)); //line at 60 degrees
  line(880, height - (3*height/9), 900, height - (3*height/9));
  line(790, (height - (height/18)) - (height-(3*height/9)), 800, (height - (height/18)) - (height-(3*height/9)));
  line(880, (height - (height/18)) - (height-(3*height/9)), 890, (height - (height/18)) - (height-(3*height/9)));
  
  line(780, height - (4*height/9), 800, height - (4*height/9)); //line at 80 degrees
  line(880, height - (4*height/9), 900, height - (4*height/9));
  line(790, (height - (height/18)) - (height-(4*height/9)), 800, (height - (height/18)) - (height-(4*height/9)));
  line(880, (height - (height/18)) - (height-(4*height/9)), 890, (height - (height/18)) - (height-(4*height/9)));
  
  line(780, height - (5*height/9), 800, height - (5*height/9)); //line at 100 degrees
  line(880, height - (5*height/9), 900, height - (5*height/9));
  line(790, (height - (height/18)) - (height-(5*height/9)), 800, (height - (height/18)) - (height-(5*height/9)));
  line(880, (height - (height/18)) - (height-(5*height/9)), 890, (height - (height/18)) - (height-(5*height/9)));
  
  line(780, height - (6*height/9), 800, height - (6*height/9)); //line at 120 degrees 
  line(880, height - (6*height/9), 900, height - (6*height/9));
  line(790, (height - (height/18)) - (height-(6*height/9)), 800, (height - (height/18)) - (height-(6*height/9)));
  line(880, (height - (height/18)) - (height-(6*height/9)), 890, (height - (height/18)) - (height-(6*height/9)));
  
  line(780, height - (7*height/9), 800, height - (7*height/9)); //line at 140 degrees
  line(880, height - (7*height/9), 900, height - (7*height/9));
  line(790, (height - (height/18)) - (height-(7*height/9)), 800, (height - (height/18)) - (height-(7*height/9)));
  line(880, (height - (height/18)) - (height-(7*height/9)), 890, (height - (height/18)) - (height-(7*height/9)));
  
  line(780, height - (8*height/9), 800, height - (8*height/9)); //line at 160 degrees 
  line(880, height - (8*height/9), 900, height - (8*height/9));
  line(790, (height - (height/18)) - (height-(8*height/9)), 800, (height - (height/18)) - (height-(8*height/9)));
  line(880, (height - (height/18)) - (height-(8*height/9)), 890, (height - (height/18)) - (height-(8*height/9)));
  
  line(780, height - (9*height/9), 800, height - (9*height/9)); //line at 180 degrees 
  line(880, height - (9*height/9), 900, height - (9*height/9));
  line(790, (height/18), 800, (height/18));
  line(880, (height/18), 890, (height/18));
  
  
// draw line indicating what number user stops at on square bar graph

 scaledinput2 = map(numbersensitivity, 0, 10, 0, height);
 strokeWeight(8);
 stroke(204, 102, 0);
 line((540), (height-scaledinput2), (660), (height-scaledinput2));
 strokeWeight(2);
 stroke(0);
 
  
 // insert buzzer for square bar graph roll if audio is on
 
 //if (numbersensitivity > 0 && numbersensitivity < 10)
 //{
 //  scaledroll2 = map(adjustedroll, 0, 180, 0, height);
 //}
         
  
// draw line indicating what angle user inputs
 
 scaledinput = map(numbertext, 0, 180, 0, height);
 strokeWeight(8);
 stroke(204, 102, 0);
 line((780), (height-scaledinput), (900), (height-scaledinput));  
 strokeWeight(2);
 stroke(0);
 
// draw analog bar and buzzer with line 

scaledpitch2 = map(pitch, -90, 90, 0, 180);
adjustedpitch = map(scaledpitch2, 0, 180, 0, height);


if(numbertext > 0 && numbertext < 180)
{  
  if (adjustedpitch > scaledinput)
  {
    line(800, 700, 800, 0);
    line(880, 700, 880, 0);
    line(800, 700, 880, 700);
    line(800, 0, 880, 0);
    fill(255,0,0);
    strokeWeight(2);
    rect(802, height-adjustedpitch, 76, adjustedpitch);
    if (CurrentColor3 == OnColor)
    {
      buzzer2.trigger();
    }
    else if (CurrentColor4 == OffColor)
    {
    }
  }
  else 
  {
    line(800, 700, 800, 0);
    line(880, 700, 880, 0);
    line(800, 700, 880, 700);
    line(800, 0, 880, 0);
    fill(0,255,0);
    strokeWeight(2);
    rect(802, height-adjustedpitch, 76, adjustedpitch);
  }
}
else 
{
  line(800, 700, 800, 0);
  line(880, 700, 880, 0);
  line(800, 700, 880, 700);
  line(800, 0, 880, 0);
  fill(0,255,0);
  strokeWeight(2);
  rect(802, height-adjustedpitch, 76, adjustedpitch);
}


 
    
  

// bar graph with squares     
    
   if (scaledpitch2 > 0 && scaledpitch2 < 18) // one bar
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
     text("4", 600, 455);
     text("5", 600, 385);
     text("6", 600, 315);
     text("7", 600, 245);
     text("8", 600, 175);
     text("9", 600, 105);
     text("10", 600, 35);
     

   }
   else if (scaledpitch2 > 18 && scaledpitch2 < 36)  // two bars
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     rect(565, 560, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);
       

   }
   else if (scaledpitch2 > 36 && scaledpitch2 < 54) // three bars
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     rect(565, 560, 70, 70);
     rect(565, 490, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);
   }
     
   
   else if (scaledpitch2 > 54 && scaledpitch2 < 72) // four bars
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     rect(565, 560, 70, 70);
     rect(565, 490, 70, 70);
     rect(565, 420, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);
     

   }
   else if (scaledpitch2 > 72 && scaledpitch2 < 90) // five bars
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     rect(565, 560, 70, 70);
     rect(565, 490, 70, 70);
     rect(565, 420, 70, 70);
     rect(565, 350, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);
   

   }
   
   else if (scaledpitch2 > 90 && scaledpitch2 < 108) // six bars 
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     rect(565, 560, 70, 70);
     rect(565, 490, 70, 70);
     rect(565, 420, 70, 70);
     rect(565, 350, 70, 70);
     rect(565, 280, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);
     
   }
   else if (scaledpitch2 > 108 && scaledpitch2 < 126) // seven bars
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     rect(565, 560, 70, 70);
     rect(565, 490, 70, 70);
     rect(565, 420, 70, 70);
     rect(565, 350, 70, 70);
     rect(565, 280, 70, 70);
     rect(565, 210, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);
     

   }
   
   else if (scaledpitch2 > 126 && scaledpitch2 < 144) // eight bars
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     rect(565, 560, 70, 70);
     rect(565, 490, 70, 70);
     rect(565, 420, 70, 70);
     rect(565, 350, 70, 70);
     rect(565, 280, 70, 70);
     rect(565, 210, 70, 70);
     rect(565, 140, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);
     

   }
   
   else if (scaledpitch2 > 144 && scaledpitch2 < 162) // nine bars
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     rect(565, 560, 70, 70);
     rect(565, 490, 70, 70);
     rect(565, 420, 70, 70);
     rect(565, 350, 70, 70);
     rect(565, 280, 70, 70);
     rect(565, 210, 70, 70);
     rect(565, 140, 70, 70);
     rect(565, 70, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);
     
     
   }
   else if (scaledpitch2 > 162 && scaledpitch2 < 180) // ten bars
   {
     fill(0,255,0);
     stroke(0);
     rect(565, 630, 70, 70);
     rect(565, 560, 70, 70);
     rect(565, 490, 70, 70);
     rect(565, 420, 70, 70);
     rect(565, 350, 70, 70);
     rect(565, 280, 70, 70);
     rect(565, 210, 70, 70);
     rect(565, 140, 70, 70);
     rect(565, 70, 70, 70);
     rect(565, 0, 70, 70);
     fill(0);
     text("1", 600, 665);
     text("2", 600, 595);
     text("3", 600, 525);
  text("4", 600, 455);
  text("5", 600, 385);
  text("6", 600, 315);
  text("7", 600, 245);
  text("8", 600, 175);
  text("9", 600, 105);
  text("10", 600, 35);    
       
     
   }

if (scaledinput2 > 0)
{
   if (adjustedpitch > scaledinput2)
   {
     fill(255, 0, 0);
     rect(565, 10, 70, 700);
     
     if (CurrentColor3 == OnColor)
     {
       buzzer2.trigger();
     }
     else if (CurrentColor4 == OffColor)
     {
     }
   }
   else 
   {
   }
   
}
  
   
   
   // left side of cross bar section
   
   
   if (adjustedroll > 108 && adjustedroll < 126) // one bar
   {
     fill(255,0,0);
     stroke(0);
     rect(495, 350, 70, 70);
     if (CurrentColor3 == OnColor)
     {
       buzzer2.trigger();
     }
     else if (CurrentColor4 == OffColor)
     {
     }

   }
   else if (adjustedroll > 126 && adjustedroll < 144) // two bars
   {
     fill(255,0,0);
     stroke(0);
     rect(495, 350, 70, 70);
     rect(425, 350, 70, 70);
     if (CurrentColor3 == OnColor)
     {
       buzzer2.trigger();
     }
     else if (CurrentColor4 == OffColor)
     {
     }
   }
   else if (adjustedroll > 144 && adjustedroll < 162) //three bars
   {
     fill(255,0,0);
     stroke(0);
     rect(495, 350, 70, 70);
     rect(425, 350, 70, 70);
     rect(355, 350, 70, 70);
     if (CurrentColor3 == OnColor)
     {
       buzzer2.trigger();
     }
     else if (CurrentColor4 == OffColor)
     {
     }

   }
   
   else if (adjustedroll > 162 && adjustedroll < 180) //four bars
   {
     fill(255,0,0);
     stroke(0);
     rect(495, 350, 70, 70);
     rect(425, 350, 70, 70);
     rect(355, 350, 70, 70);
     rect(285, 350, 70, 70);
     if (CurrentColor3 == OnColor)
     {
       buzzer2.trigger();
     }
     else if (CurrentColor4 == OffColor)
     {
     }
   }
   
     
     // right side of cross bar section 
    
   
   if (adjustedroll > 54 && adjustedroll < 72) // one bar
   {
     fill(255,0,0);
     stroke(0);
     rect(635, 350, 70, 70);
     if (CurrentColor3 == OnColor)
     {
       buzzer2.trigger();
     }
     else if (CurrentColor4 == OffColor)
     {
     }   
   }
   else if (adjustedroll > 36 && adjustedroll < 54 ) // two bars
   {
     fill(255,0,0);
     stroke(0);
     rect(635, 350, 70, 70);
     rect(705, 350, 70, 70);
     if (CurrentColor3 == OnColor)
     {
       buzzer2.trigger();
     }
     else if (CurrentColor4 == OffColor)
     {
     }
   }
   else if (adjustedroll > 18 && adjustedroll < 36) //three bars
   {
     fill(255,0,0);
     stroke(0);
     rect(635, 350, 70, 70);
     rect(705, 350, 70, 70);
     rect(775, 350, 70, 70);
     if (CurrentColor3 == OnColor)
     {
       buzzer2.trigger();
     }
     else if (CurrentColor4 == OffColor)
     {
     }
   }
   
   else if (adjustedroll > 0 && adjustedroll < 18) //four bars
   {
     fill(255,0,0);
     stroke(0);
     rect(635, 350, 70, 70);
     rect(705, 350, 70, 70);
     rect(775, 350, 70, 70);
     rect(845, 350, 70, 70);
     if (CurrentColor3 == OnColor)
     {
       buzzer2.trigger();
     }
     else if (CurrentColor4 == OffColor)
     {
     }
   }
   
float rollfortext = map(adjustedroll, 0, 180, 90, -90);
   
   if (timer.isRunning())
   {
       output.println(rollfortext + ", " + scaledpitch2 + ", " + millis());
   }
  
   
}

void Angle()
{
  text = cp5.get(Textfield.class,"setangle").getText();
  numbertext = float(text);  
}

void Start()
{
  time = cp5.get(Textfield.class,"timing").getText();
  longnumbertimer = Long.parseLong(time);    
  adjustedtimer = longnumbertimer * 1000;
  timer.configure(100, adjustedtimer);
  timer.start();
  timertext = "Timer has started...";
  output = createWriter("rollvalues" + "_" + month() + "_" + day() + "_" + year() + "_" + hour() + "_" + minute() + ".txt");
}

void Reset()
{
  time = cp5.get(Textfield.class,"timing").getText();
  longnumbertimer = Long.parseLong(time);
  timertext = "Timer has been reset...";
  timerCallbackInfo = "Time Remaining: " + time + " s";
  timer.stop(CountdownTimer.StopBehavior.STOP_IMMEDIATELY);
  timer.reset(CountdownTimer.StopBehavior.STOP_IMMEDIATELY);
  output.flush();
  output.close();
}
  

void Number()
{
  sensitivity = cp5.get(Textfield.class,"Sensitive").getText();
  numbersensitivity = float(sensitivity);

}

void update(int x, int y) 
{
   if (overStableOn(StableXOn, StableYOn, StableSize*2, StableSize))
   {
    StableOverOn = true;
    StableOverOff = false;
   }
    
   else if (overStableOff(StableXOff, StableYOff, StableSize*2, StableSize))
   {
    StableOverOn = false;
    StableOverOff = true;
   }

   else 
   {
     StableOverOn = StableOverOff = false;
   }
}

boolean overStableOn(int x, int y, int width, int height)  
{
  if (mouseX >= x && mouseX <= x+width && 
      mouseY >= y && mouseY <= y+height) {
    return true;
  } else {
    return false;
  }
}

boolean overStableOff(int x, int y, int width, int height)  
{
  if (mouseX >= x && mouseX <= x+width && 
      mouseY >= y && mouseY <= y+height) {
    return true;
  } else {
    return false;
  }
}

void mousePressed() {
  
  if (StableOverOn) 
  {
    CurrentColor3 = OnColor;
    CurrentColor4 = NeutralColor;
  }
  
  if (StableOverOff)
  {
    CurrentColor3 = NeutralColor;
    CurrentColor4 = OffColor;
  }
     
}

void serialEvent(Serial myPort)
{
  imu = myPort.readString();
}

void onTickEvent(CountdownTimer t, long timeLeftUntilFinish) 
{
  timerCallbackInfo = "Time Remaining: " + (timeLeftUntilFinish/1000) + " s";
}

void onFinishEvent(CountdownTimer t) 
{
  timerCallbackInfo = "Time Remaining: [finished]";
  timertext = "Timer is done.";
  output.flush();
  output.close();
}

