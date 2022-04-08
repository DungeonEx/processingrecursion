// STUDENT 5%: Complete this comment block, including your name & blank entries.
/************************************************************
/* Sketch: CSC220Fall2021Final5Maze, final "exam" project.
/* Author: Thomas Pham
/* Creation Date: 11/17/2021
/* Due Date: Friday 12/10/2021
/* Course: CSC 220 - 020
/* Professor Name: Dr. Parson
/* Assignment: 5.
/* Purpose: Tunnel a 2D maze, either interactively or semi-automatically.
*************************************************************/

/* POLLED KEYS IN keyPolled().
/* THESE KEYS ARE POLLED IN FUNCTION keyPolled() to do the following actions.
/* NOTE : RIGHT, LEFT, UP, and DOWN arrows must be ignored when excavator is isAutoMode. 
/* RIGHT ARROW moves the excavator 1 pixel to the right, allows maze completion out right side.
   DO NOT MOVE THE EXCAVATOR OFF SCREEN, AND FOR ALL DIRECTIONS EXCEPT RIGHT, NEVER LET IT
   GO PAST WallSize PIXELS AWAY FROM THE left, top, or bottom edge of display.
/* LEFT ARROW moves the excavator 1 pixel to the right, stops when within WallSize of x==0.
/* UP ARROW moves the excavator 1 pixel up, stops when within WallSize of y==0.
/* DOWN ARROW moves the excavator 1 pixel down, stops when within WallSize of y==height-1.

/* NON-POLLED KEYS IN keyPressed().
/* 'a' puts excavator in isAutoMode mode.
*/

int excavatorX, excavatorY ;
boolean isAutoMode = false ;
int autoModeXspeed = 0, autoModeYspeed = 0, autoModeXendpoint = 0, autoModeYendpoint = 0 ;
final int WallSize = 25 ;  // Do not go beyond WallSize*2 except to tunnel out to right side.
// STUDENT 5% Set your own spaceColor & wallColor that differ from mine, using RGB
final int spaceColor = color(0, 255, 255);  // Color outside the maze in RGB, and tunnel color.
final int wallColor = color(255, 255, 0);   // Color of the walls.
PImage excavator = null ;

void setup() {
  size(1000, 1000, P2D);    // STUDENT may adjust size to fit monitor or use fullScreen(P2D);
  frameRate(60);            // for newer Mac bug
  excavatorX = WallSize/2 ;         // tunnel in from left
  excavatorY = int(random(WallSize*2, height-WallSize*2));
  background(spaceColor);
  rectMode(CORNER);
  fill(wallColor);
  stroke(0);
  rect(WallSize, WallSize, width-WallSize*2, height-WallSize*2);
  noStroke();
  imageMode(CENTER);
  // STUDENT 5% load your image file into excavator.
  excavator = loadImage("snow.png");
}

boolean firstTime = true ; // ADDED 12/1 see start of draw() function below
void draw() {
  /* STUDENT 30% of project:
    1. set the fill color to spaceColor, with no stroke.
    2. if sketch is in isAutoMode mode
        if excavatorX equals autoModeXendpoint and excavatorY equals autoModeYendpoint
            set isAutoMode to false
        else
            add autoModeXspeed into excavatorX
            add autoModeYspeed into excavatorY
    3. Draw a rectangle centered at excavatorX, excavatorY with width & height of WallSize
    4. Draw excavator image at excavatorX, excavatorY with width & height a fraction of WallSize
        Your image must fit fully inside the rectangle in which it is centered.
    5. Call function keyPolled.
  */
  

   if (firstTime) {
    // Added 12/1 because of a bug in at least one Processing installation.
    // This was already done in setup(), but at least one student's
    // Processing system is only displaying the rect(...) from setup
    // in a quick flash. Displaying it the first time in draw() fixes
    // the problem for that student, so:
    rectMode(CORNER);
    fill(wallColor);
    stroke(0);
    rect(WallSize, WallSize, width-WallSize*2, height-WallSize*2);
    noStroke();
    firstTime = false ;
  }
  fill(spaceColor);
  noStroke();
  
  if(isAutoMode == true){
    
    if(excavatorX == autoModeXendpoint && excavatorY == autoModeYendpoint){
     isAutoMode=false;       
    }
    else{
     excavatorX+=autoModeXspeed; 
     excavatorY+=autoModeYspeed; 
    }    
  }
  
  rectMode(CENTER);
  rect(excavatorX,excavatorY,WallSize,WallSize);
  //rect(50,50,100,100);

  image(excavator,excavatorX,excavatorY,WallSize*.9,WallSize*.9);
  keyPolled();
}

void keyPolled() {
  if (keyPressed) {
    /* START OF STUDENT CODE, 25% of project:
      If the key is coded and sketch is NOT already in isAutoMode
          If it is LEFT
            set excavatorX to excavatorX-1,
                constrained to range min(excavatorX,WallSize*2) and width-1
          Else if it is RIGHT
            set excavatorX to excavatorX+1,
                constrained to range 0 and width-1
          Else if it is UP
            set excavatorY to excavatorY-1,
                constrained to range WallSize*2 and height-WallSize*2
          Else if it is DOWN
            set excavatorY to excavatorY+1,
                constrained to range 0 and height-WallSize*2
     */
     if(key == CODED && isAutoMode == false){
       if (keyCode == LEFT){
         excavatorX= constrain(excavatorX-1,min(excavatorX,WallSize*2),width-1);   
         println("excavatorX" + excavatorX);
       }
       if (keyCode == RIGHT){
         excavatorX= constrain(excavatorX+1,0,width-1);      
         println("excavatorX" + excavatorX);
       } 
       if (keyCode == UP){
         excavatorY= constrain(excavatorY-1,WallSize*2,height-WallSize*2);      
         println("excavatorY" + excavatorY);
       } 
       if (keyCode == DOWN){
         excavatorY= constrain(excavatorY+1,0,height-WallSize*2);      
         println("excavatorY" + excavatorY);
       }
     }
     
     
  }
}

int [][] XYdeltas = {
  {-1, 0},  // left
  {0, -1},  // up
  {1, 0},   // right
  {0, 1}    // down
};

void keyPressed() {
  /* STUDENT CODE, 30% of project:
    If the key is 'a' and sketch is NOT already in isAutoMode
      Set global isAutoMode to true
      Initialize local int XYdeltaIndex to a random number between 0 and XYdeltas.length-1
      Set global autoModeXspeed to XYdeltas[XYdeltaIndex][0]
      Set global autoModeYspeed to XYdeltas[XYdeltaIndex][1]
      If autoModeXspeed is not equal to 0
        Set autoModeYendpoint equal to excavatorY
        Set autoModeXendpoint equal to excavatorX
            PLUS (autoModeXspeed TIMES a random number between WallSize and WallSize*10)
        If autoModeXendpoint is less than (the smaller of WallSize*2 and excavatorX)
          Set autoModeXendpoint to (the smaller of WallSize*2 and excavatorX)
        Else if autoModeXendpoint is greater than or equal to width of the display
          Set autoModeXendpoint to width-1
          If excavatorX is greater than or equal to width of the display
            Set excavatorX to width-1
      Else // autoModeXspeed is equal to 0
        Set autoModeXendpoint equal to excavatorX
        Set autoModeYendpoint equal to excavatorY
            PLUS (autoModeYspeed TIMES a random number between WallSize and WallSize*10)
        If autoModeYendpoint is less than (the smaller of WallSize*2 and excavatorY)
          Set autoModeYendpoint to (the smaller of WallSize*2 and excavatorY)
        Else if autoModeYendpoint is greater than or equal to height-WallSize*2
          Set autoModeYendpoint to the larger of height-WallSize*2 and excavatorY
  */
  if(keyPressed){
    if(key == 'a' && isAutoMode !=true){
      isAutoMode = true;
      println("isAutoMode is " + isAutoMode);
      int XYdeltaIndex = int(random(0,XYdeltas.length-1));    
      autoModeXspeed= XYdeltas[XYdeltaIndex][0];
      autoModeYspeed= XYdeltas[XYdeltaIndex][1];
      if(autoModeXspeed != 0){
        autoModeYendpoint = excavatorY;  
        //autoModeXendpoint = excavatorX  
        //  + autoModeXspeed * (int)random(WallSize,WallSize*10);
        autoModeXendpoint = int(excavatorX + (autoModeXspeed * random(WallSize,WallSize*10)));  
        if(autoModeXendpoint < min(WallSize*2,excavatorX)){
            autoModeXendpoint = min(WallSize*2,excavatorX);         
        }
        else if(autoModeXendpoint >= width){
          autoModeXendpoint = width-1;
          if(excavatorX >= width){
            excavatorX = width-1;            
          }          
        }
      }
     
      else{ //autoModeXspeed is 0
        autoModeXendpoint = excavatorX;
        //autoModeYendpoint = excavatorX  
        //  + autoModeYspeed * (int)random(WallSize,WallSize*10);       
        autoModeYendpoint = int(excavatorY + (autoModeYspeed * random(WallSize,WallSize*10)));
        if(autoModeYendpoint < min(WallSize*2,excavatorY)){
            autoModeYendpoint = min(WallSize*2,excavatorY);         
        }
        else if(autoModeYendpoint >= height-WallSize*2){
            autoModeYendpoint = max(height-WallSize*2,excavatorY);        
        
        }
      }
    }
  }
}
