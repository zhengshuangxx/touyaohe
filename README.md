# touyaohe
#include <Servo.h>
#include <IRremote.h>
int RECV_PIN=4;//红外接收引脚4
IRrecv irrecv(RECV_PIN);//定义红外接收对象
Servo myservo;
decode_results results;    


int pos=0;

void setup() 
{
  //Serial.begin(9600);
  myservo.attach(A1);//定义舵机的引脚
  irrecv.enableIRIn();//启动红外接收
}

void loop() 
{
  if (irrecv.decode(&results))//如果解码成功（接收到红外信号）
  {
   myservo.write(60);//舵机角度为60（盒盖关闭）
   delay(10000);     //宠物离开后10秒盒子才会重新打开，避免使宠物对投药盒产生好奇
  }
  else             //未接收到信号
  {
     myservo.write(0);//舵机角度为0（盒盖打开）
  }
 
  irrecv.resume();
  delay(100);//延迟0.1秒
}
