## Lab 7 
# การทดลองเปลี่ยนแปลงเพิ่มเติมโคดในการทำงานของ ไมโครคอนโทลเลอร์
# ซอสโคดหรือโปรแกรมที่ได้แก่ไขนี้ เป็นโปรแกรมที่ใช้ในการเขียนใส่ในไมโครคอนโทรเลอร์ เพื่อใช้ในการค้นหาสัญญาณไวไฟ โดยเมื่อรันโปนแกรมลงบนไมโครคอนโทรเลอร์แร้ว ตัวไมโครคอนโทลเลอร์จะสามารถนำไปใช้ในการค้นหาไวไฟได้ โดยจะแสดงรายละเอียดตามซอสโคดที่เขียนลงไป

#include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	WiFi.mode(WIFI_STA);
	WiFi.disconnect();
	delay(100);
	Serial.println("\n\n\n");
}

void loop()
{
	cnt++;
	Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");
	int n = WiFi.scanNetworks();
	if(n == 0) {
		Serial.println("NO NETWORK FOUND");
	} else {
		for(int i=0; i<n; i++) {
			Serial.print(i + 1);
			Serial.print(": ");
			Serial.print(WiFi.SSID(i));
			Serial.print(" (");
			Serial.print(WiFi.RSSI(i));
			Serial.println(")");
			Serial.print(WiFi.channel(i));
			Serial.print(BSSID(i));
			delay(10);
		}
	}
	Serial.println("\n\n");
	int c = cnt %4 + 9;
	int s = c * 1000;
	delay(s);
