
//PULSOGAME
//AÑO 2015
//VERSION: 1.0 
//Autor: Hiroshi Takey Franco
//Modificado por: Walter Mauricio Mauricio Matinez Nogales 

#include "pitches.h"

const int gameover[] = {15,                                               // Array for Game over song
  NOTE_C4, 8, NOTE_H, 8, NOTE_H, 8, NOTE_G3, 8, NOTE_H, 4, NOTE_E3, 4, NOTE_A3, 6, NOTE_B3, 6, NOTE_A3, 6, NOTE_GS3, 6, NOTE_AS3, 6, NOTE_GS3, 6, NOTE_G3, 8, NOTE_F3, 8, NOTE_G3, 4};

int melody[] = {
  NOTE_E7, NOTE_E7, 0, NOTE_E7, 0, NOTE_C7, NOTE_E7, 0, NOTE_G7, 0, 0,  0, NOTE_G6, 0, 0, 0, NOTE_C7, 0, 0, NOTE_G6, 0, 0, NOTE_E6, 0, 0, NOTE_A6, 0, NOTE_B6, 0, NOTE_AS6, NOTE_A6, 0, 
  NOTE_G6, NOTE_E7, NOTE_G7, NOTE_A7, 0, NOTE_F7, NOTE_G7, 0, NOTE_E7, 0,NOTE_C7, NOTE_D7, NOTE_B6, 0, 0,NOTE_C7, 0, 0, NOTE_G6, 0, 0, NOTE_E6, 0, 0, NOTE_A6, 0, NOTE_B6, 0, NOTE_AS6, NOTE_A6, 0, 
  NOTE_G6, NOTE_E7, NOTE_G7, NOTE_A7, 0, NOTE_F7, NOTE_G7, 0, NOTE_E7, 0,NOTE_C7, NOTE_D7, NOTE_B6, 0, 0,

    NOTE_E7, NOTE_E7, 0, NOTE_E7, 
  0, NOTE_C7, NOTE_E7, 0,
  NOTE_G7, 0, 0, 0,
  NOTE_G6, 0, 0, 0, 

  NOTE_C7, 0, 0, NOTE_G6, 
  0, 0, NOTE_E6, 0, 
  0, NOTE_A6, 0, NOTE_B6, 
  0, NOTE_AS6, NOTE_A6, 0, 

  NOTE_G6, NOTE_E7, NOTE_G7, 
  NOTE_A7, 0, NOTE_F7, NOTE_G7, 
  0, NOTE_E7, 0, NOTE_C7, 
  NOTE_D7, NOTE_B6, 0, 0,

  NOTE_C7, 0, 0, NOTE_G6, 
  0, 0, NOTE_E6, 0, 
  0, NOTE_A6, 0, NOTE_B6, 
  0, NOTE_AS6, NOTE_A6, 0, 

  NOTE_G6, NOTE_E7, NOTE_G7, 
  NOTE_A7, 0, NOTE_F7, NOTE_G7, 
  0, NOTE_E7, 0, NOTE_C7, 
  NOTE_D7, NOTE_B6, 0, 0
};
//Mario main them tempo
int tempo[] = {
  12, 12, 12, 12,12, 12, 12, 12, 12, 12, 12, 12,12, 12, 12, 12, 12, 12, 12, 12,12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 9, 9, 9, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12,
  12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 9, 9, 9, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12,
};

const int ledPin =  13; 
unsigned long tiempo = 0; 
unsigned long tiempo1 = 0;
unsigned long tiempo2 = 0; 
unsigned long tiempo3 = 0; 
unsigned long t_actualizado = 0;
unsigned long t_delay = 1000;

const byte lineajuego = A0;
const byte lineameta = A1;
const byte timer = A2;

const byte led = 12;
const byte piezowinlos = A4;
const byte piezowinlos1 = A5;

int lineajueg = 0;

int melody2[] = {NOTE_C4, NOTE_G3,NOTE_G3, NOTE_A3, NOTE_G3,0, NOTE_B3, NOTE_C4};

int noteDurations[] = { 4, 8, 8, 4,4,4,4,4 };

//__________DEFINICION DE FRECUENCIA DEL TONO DE MARIO Y VELOCIDAD__________________________________________
void buzz(int targetPin, long frequency, long length) 
{
  long delayValue = 1000000/frequency/2; // calculate the delay value between transitions
  long numCycles = frequency * length/ 1000; // calculate the number of cycles for proper timing
  for (long i=0; i < numCycles; i++) {digitalWrite(targetPin,HIGH); delayMicroseconds(delayValue); digitalWrite(targetPin,LOW); delayMicroseconds(delayValue);}
}

//________________MUSIK MARIO_______________________________________________
void segundo()
{
  int size = sizeof(melody) / sizeof(int);
  for (int thisNote = 0; thisNote < size; thisNote++) 
   {
    int noteDuration = 1000/tempo[thisNote]; buzz(piezowinlos, melody[thisNote],noteDuration);
    int pauseBetweenNotes = noteDuration;
    delay(pauseBetweenNotes);
    buzz(piezowinlos, 0,noteDuration);
//_______________SI TOCO EL ALAMBRE _____________________________________________
    if (digitalRead(lineajuego) == 0) {perdist();}
//_____________SI LLEGO A LA META_______________________________________     
    if (digitalRead(lineameta) == 0) {ganee();}
           tiempo = millis();
  if(tiempo > t_actualizado + t_delay) {t_actualizado = tiempo; digitalWrite(ledPin, !digitalRead(ledPin));}
  }}

//_________________________________________________________________________
void segundoo()
{
//________________MUSIK MARIO Acelerada______________________________________
  int size = sizeof(melody) / sizeof(int);
  for (int thisNote = 0; thisNote < size; thisNote++) 
   { 
    int noteDuration = 666.6/tempo[thisNote]; buzz(piezowinlos, melody[thisNote],noteDuration);
    int pauseBetweenNotes = noteDuration * 1.00;
    delay(pauseBetweenNotes); buzz(piezowinlos, 0,noteDuration);    
//_______________SI TOCO EL ALAMBRE _____________________________________________
    if (digitalRead(lineajuego) == 0){perdist();}
//_____________SI LLEGO A LA META_______________________________________     
    if (digitalRead(lineameta) == 0){ganee();}
       tiempo = millis();
  if(tiempo > t_actualizado + t_delay) {t_actualizado = tiempo; digitalWrite(ledPin, !digitalRead(ledPin));}
  }}
  
//________________MUSIK MARIO Acelerada al hard______________________________________
void segundooo()
{
  int size = sizeof(melody) / sizeof(int);
  for (int thisNote = 0; thisNote < size; thisNote++) 
   { 
    int noteDuration = 333.3/tempo[thisNote]; buzz(piezowinlos, melody[thisNote],noteDuration);
    int pauseBetweenNotes = noteDuration * 0.80;
    delay(pauseBetweenNotes); buzz(piezowinlos, 0,noteDuration);
//_______________SI TOCO EL ALAMBRE _____________________________________________
    if (digitalRead(lineajuego) == 0){perdist();}
//_____________SI LLEGO A LA META_______________________________________     
    if (digitalRead(lineameta) == 0){ganee();}
    }}
    
//_____________SI TE ACABO EL TIEMPO_______________________________________ 
void perdist()
{
    for (int thisNote = 1; thisNote < (gameover[0] * 2 + 1); thisNote = thisNote + 2) 
    {
      // Run through the notes one at a time
    tone(piezowinlos, gameover[thisNote], (1000/gameover[thisNote + 1]));// Play the single note
    delay((1000/gameover[thisNote + 1]) * 1.30); noTone(piezowinlos);
    }
    yaa();
}
//_____________SI LLEGUE AL FINAL_______________________________________ 
void ganee()
{
      for (int thisNote = 0; thisNote < 8; thisNote++) 
      {
        int noteDuration = 1000/noteDurations[thisNote];
        tone(piezowinlos, melody2[thisNote],noteDuration);

        int pauseBetweenNotes = noteDuration * 1.30;
        delay(pauseBetweenNotes); noTone(piezowinlos);
      }
       yaa();
    }
//_____________PARA VOLVER A JUGAR_______________________________________ 
void yaa()
{
  while(1){
    if (digitalRead(timer) == 0){digitalWrite(led,LOW); digitalWrite(13,LOW);}
    loop();}
}
//________________________________________________________________
void setup()
{ 
  pinMode(piezowinlos, OUTPUT);
  pinMode(led, OUTPUT);
  pinMode(ledPin, OUTPUT); 
  
  pinMode(lineajuego, INPUT_PULLUP);
  pinMode(lineameta, INPUT_PULLUP);
  pinMode(timer, INPUT_PULLUP);
}
//_____________________________
void loop()
{
  if (digitalRead(timer) == 0){   
  digitalWrite(led,LOW);
  segundo();
  digitalWrite(led,HIGH);
  segundoo();
  digitalWrite(led,LOW);
  segundooo();
  perdist();}
}


     

