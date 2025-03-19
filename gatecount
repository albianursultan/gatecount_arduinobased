
#include <LiquidCrystal_I2C.h> ///Library yang dibutuhkan///
#include <Wire.h>
#include <Servo.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

const int trigpin = 7;
const int echopin = 8;

#define buzzer 5    ///define pin
#define rLED  10    
#define gLED  9
#define LED   8
#define button 13
#define IR 12
#define ldr A3 


int distance;       ///variabel jarak untuk ultrasonik
int duration;       ///variabel durasi untuk ultrasonik

int vehicle;        ///variabel kendaraan masuk

int buttonState = 0; 
int inprared;


int pos = 45;       ///sudut default motor servo yang difungsikan untuk palang
Servo servo;        ///variabel servo

void dekat();     /// perintah yang di jalankan saat ada objek terdeteksi di ultrasonik
void dekat(){
  pinMode(rLED, OUTPUT);
  digitalWrite(rLED, HIGH);
  lcd.setCursor(0, 0);
  lcd.print("=====Welcome======"); ///tampilan lcd 
  lcd.setCursor(0, 1);
  lcd.print("Push the Button");   
  delay(1000);
}

void menyala ();
void menyala (void){
  pinMode(ldr, INPUT); 
  pinMode(LED, OUTPUT);
  digitalWrite(LED, HIGH);
  delay(1000);  
}

void masuk ();    /// perintah yang dijalankan saat push button di tekan
void masuk(void)
{
    pinMode(gLED,OUTPUT);      ///define led as an output
    pinMode(buzzer ,OUTPUT);  ///define buzzer as an output
    pinMode(button, OUTPUT);
    servo.write(140);         ///sudut servo menjadi 140 derajat dan palang terbuka                        
    digitalWrite(gLED, HIGH);    ///lampu led menyala
    digitalWrite(buzzer, HIGH);    ///buzzer menyala 
    delay(100);
    digitalWrite(buzzer, LOW);
    delay(100);
    digitalWrite(buzzer, HIGH);
    delay(100);
    digitalWrite(buzzer, LOW);
    lcd.clear();
    lcd.setCursor(0,0);
    lcd.print("Silahkan Masuk"); ///tampilan lcd
    delay(3000);
    digitalWrite(36, LOW);     /// led mati   
    delay(5000);   
    servo.write(50);          ///palang kembali tertutup   
}

void setup(){
  Serial.begin(9600);
  servo.attach(3);            ///pin servo   
  servo.write(pos);  
          ///servo ke sudut default saat alat dinyalakan
  pinMode (trigpin, OUTPUT);  ///define Trigger pin ultrasonic as an output
  pinMode (echopin, INPUT);   ///define echo pin as an input
  lcd.begin(16, 2);           ///setup lcd
  lcd.init();
  lcd.setBacklight(1);
  lcd.display();
  delay(500);
  lcd.setCursor(1, 0);
  lcd.print(("Smart Portal"));
  delay(1000); 
  lcd.setCursor(5, 1);
  lcd.print("Ticket");
  delay(2000);   
  lcd.clear();   

}
  void loop () {

  byte  buttonState = digitalRead(button);
  Serial.println(buttonState);
 
  digitalWrite(trigpin, HIGH); ///perintah ultrasonic untuk memantulkan suara untuk detect jarak 
  delayMicroseconds(10);
  digitalWrite(trigpin, LOW);
  delayMicroseconds(10);
  
  duration = pulseIn(echopin, HIGH); ///waktu di peroleh dari data yang di terima echo pin
  distance = (duration*.0343)/2;     ///rumus jarak (waktu x kecepatan/2)
  lcd.clear();

  int ldrval = analogRead(ldr);
  Serial.println(ldrval);


  if (distance < 10)
  {
    dekat ();   ///void dekat akan jalan ketika jarak di bawah 10 cm
  }

  else if (distance > 10)
  {
  Serial.print("Jarak :");
  Serial.print(distance);
  Serial.print(" CM");
  lcd.setCursor(0, 0);         ///lcd yang akan tertampil ketika mendeteksi objek diatas 10 cm / tidak mendeteksi apa apa
  lcd.print("Vehicle Parked qty:");
  lcd.setCursor(6,1);
  lcd.print(vehicle);
  delay(1000); 
  }

  if(buttonState == HIGH){
    masuk ();
  }
  else if (buttonState == LOW){
  dekat();
  }

  if (ldrval > 10){
    digitalWrite(LED, HIGH);
    delay(1000);
  }
  }

  ///trial n error : sudut servo & ldr value
