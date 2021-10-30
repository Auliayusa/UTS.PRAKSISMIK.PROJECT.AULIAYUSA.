# UTS.PRAKSISMIK.PROJECT.AULIAYUSA.

#include <IRremote.h>
//motor penggerak robot
int kiri1 = 13;
int kiri2 = 12;
int kanan1 = 9;
int kanan2 = 8;
int en1 = 11;
int en2 = 10;

//sensor infrared TSOP remote TV
int sensor = 2;
IRrecv irrecv(sensor);
decode_results data;

void setup()
{
  Serial.begin(9600);
  irrecv.enableIRIn();
  
//Mulai menerima data
  pinMode(kiri1,OUTPUT);
  pinMode(kiri2,OUTPUT);
  pinMode(kanan1,OUTPUT);
  pinMode(kanan2,OUTPUT);
  pinMode(en1,OUTPUT);
  pinMode(en2,OUTPUT);
}
void loop()
{
  if(irrecv.decode(&data))
  {
    Serial.println(data.value);
    irrecv.resume();
  //Terima data selanjutnya
    analogWrite(en1,255);
    analogWrite(en2,255);
  
  if(data.value==16591063)
  //belok kiri
  {
    digitalWrite(kiri1,LOW);
    digitalWrite(kiri2,HIGH);
    digitalWrite(kanan1,HIGH);
    digitalWrite(kanan2,LOW);
    Serial.println("Belok Kiri");
  }
  else if(data.value==16607383)
  //belok kanan
  {
    digitalWrite(kiri1,HIGH);
    digitalWrite(kiri2,LOW);
    digitalWrite(kanan1,LOW);
    digitalWrite(kanan2,HIGH);
    Serial.println("Belok Kanan");
  }
  else if(data.value==16615543)
  //maju
  {
    digitalWrite(kiri1,LOW);
    digitalWrite(kiri2,HIGH);
    digitalWrite(kanan1,LOW);
    digitalWrite(kanan2,HIGH);
   	Serial.println("Maju");
  }
  else if(data.value==16619623)
  //mundur
  {
    digitalWrite(kiri1,HIGH);
    digitalWrite(kiri2,LOW);
    digitalWrite(kanan1,HIGH);
    digitalWrite(kanan2,LOW);
    Serial.println("Mundur");
  }
  else
  //diam
  {
    digitalWrite(kiri1,LOW);
    digitalWrite(kiri2,LOW);
    digitalWrite(kanan1,LOW);
    digitalWrite(kanan2,LOW);
    Serial.println("Diam");
  }
 }
}
