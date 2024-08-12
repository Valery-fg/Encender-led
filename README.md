/*
Cuando se refiere a serial, es la comuncicaión entre arduino y la computadora.
Cuando se refiere a myBT, es la comunicación entre arduino y el modulo.
*/
#include<SoftwareSerial.h>                            //incluir libreria para utilizar los comandos del modulo bluetooth.
SoftwareSerial myBT(10,11);                           //Pin de conexión RX-->pin 11, TX-->pin 10.

void setup(){
  Serial.begin(9600);                                 //Inicializar comunicación serial para ver y enviar los comandos AT(debe estar en 9600 baudios en el serial monitor)
  Serial.print("Monitor serial preparado.");          //Mensaje para confirmar comunicación serie.
  myBT.begin(38400);                                  //Inicializar velocidad de comunicación del modulo bluetooth.
}
void loop(){
  if(myBT.available()){                               //Devuelve verdadero cuando hay datos disponibles desde el modulo.
    Serial.write(myBT.read());                        //Se escribe en el monitor serial el dato obtenido del modulo HC05. (Lectura de BT y envia a Arduino)
  }
  if(Serial.available()){                             //Cuando hay información disponible en el monitor serial, se envia al modulo.
    myBT.write(Serial.read());                        //lectra de Arduino y envio a BT.
  }

}
