---
author: fangrenbin
comments: true
date: 2012-12-19 15:53:03+00:00
layout: post
slug: arduino-ethernet-shield-control-led
title: arduino ethernet shield通过网页来控制LED
wordpress_id: 420
categories:
- arduino
---

通过网页来控制LED开关的小实验。
素材：arduino, arduino ethernet shield, 3 led, 3 220Ω电阻，网线，连接线若干，面包板。
电路图：

[![Untitled Sketch_bb](http://frb.name/wp-content/uploads/2012/12/Untitled-Sketch_bb_thumb.png)](http://frb.name/wp-content/uploads/2012/12/Untitled-Sketch_bb.png)

[![IMG-20121219-00051](http://frb.name/wp-content/uploads/2012/12/IMG-20121219-00051_thumb.jpg)](http://frb.name/wp-content/uploads/2012/12/IMG-20121219-00051.jpg)

[![led](http://frb.name/wp-content/uploads/2012/12/led_thumb.png)](http://frb.name/wp-content/uploads/2012/12/led1.png)

程序源代码：

    
    #include 
    #include 
    
    byte mac[] = {
      0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
    IPAddress ip(192, 168, 3, 149);
    
    EthernetServer server(80);
    
    int redLEDpin = 7;
    int blueLEDpin = 8;
    int greenLEDpin = 9;
    
    String readString = String(30);
    String redLEDState = String(3);
    String blueLEDState = String(3);
    String greenLEDState = String(3);
    
    void setup(){
      Serial.begin(9600);
      while(!Serial){
        ;//wat for serial prot to connect need for lenoardo only
      }
      Ethernet.begin(mac, ip);
      server.begin();
    
      Serial.print("Server is at:");
      Serial.println(Ethernet.localIP());
    
      pinMode(redLEDpin, OUTPUT);
      pinMode(blueLEDpin, OUTPUT);
      pinMode(greenLEDpin, OUTPUT);
    
      digitalWrite(redLEDpin, LOW);
      digitalWrite(blueLEDpin, LOW);
      digitalWrite(greenLEDpin, LOW);
    
      redLEDState = "OFF";
      blueLEDState = "OFF";
      greenLEDState = "OFF";
    }
    
    void loop(){
      EthernetClient client = server.available();
      if(client){
        boolean currentLineIsBlank = true;
        while(client.connected()){
          if(client.available()){
    
            char c = client.read();
            Serial.print(c);
            if(readString.length() < 30){
              readString.concat(c);
            }
    
            if(c == '\n' && currentLineIsBlank){
              int redLED = readString.indexOf("redLED=");
              if(readString.substring(redLED,redLED+9) == "redLED=ON"){
                digitalWrite(redLEDpin, HIGH);
                Serial.println("red LED IS ON");
                redLEDState = "ON";
              }
              else if(readString.substring(redLED, redLED+10) == "redLED=OFF"){
                digitalWrite(redLEDpin, LOW);
                Serial.println("red LED IS OFF");
                redLEDState = "OFF";
              }
    
              int blueLED = readString.indexOf("blueLED=");
              if(readString.substring(blueLED,blueLED+10) == "blueLED=ON"){
                digitalWrite(blueLEDpin, HIGH);
                Serial.println("blue LED IS ON");
                blueLEDState = "ON";
              }
              else if(readString.substring(blueLED, blueLED+11) == "blueLED=OFF"){
                digitalWrite(blueLEDpin, LOW);
                Serial.println("blue LED IS OFF");
                blueLEDState = "OFF";
              }
    
              int greenLED = readString.indexOf("greenLED=");
              if(readString.substring(greenLED,greenLED+11) == "greenLED=ON"){
                digitalWrite(greenLEDpin, HIGH);
                Serial.println("green LED IS ON");
                greenLEDState = "ON";
              }
              else if(readString.substring(greenLED, greenLED+12) == "greenLED=OFF"){
                digitalWrite(greenLEDpin, LOW);
                Serial.println("green LED IS OFF");
                greenLEDState = "OFF";
              }
              // html start
              client.println("HTTP/1.1 200 OK");
              client.println("Content-Type: text/html");
              client.println();
    
              // red led
              client.println("<span>RED</span> LED is");
              client.print(redLEDState);
              client.print("--->");
    
              if(redLEDState == "ON"){
                client.println("<a href="\"./?redLED=OFF\"">Turn OFF</a>");
                client.println("
    ");
              }else if(redLEDState == "OFF"){
                client.println("<a href="\"./?redLED=ON\"">Turn ON</a>");
                client.println("
    ");
              }
    
              //blue led
              client.println("<span>BLUE</span> LED is");
              client.print(blueLEDState);
              client.print("--->");
    
              if(blueLEDState == "ON"){
                client.println("<a href="\"./?blueLED=OFF\"">Turn OFF</a>");
                client.println("
    ");
              }else if(blueLEDState == "OFF"){
                client.println("<a href="\"./?blueLED=ON\"">Turn ON</a>");
                client.println("
    ");
              }
    
              //green led
              client.println("<span>GREEN</span> LED is");
              client.print(greenLEDState);
              client.print("--->");
    
              if(greenLEDState == "ON"){
                client.println("<a href="\"./?greenLED=OFF\"">Turn OFF</a>");
                client.println("
    ");
              }else if(greenLEDState == "OFF"){
                client.println("<a href="\"./?greenLED=ON\"">Turn ON</a>");
                client.println("
    ");
              }
    
              break;
            }
    
            if(c == '\n'){
              currentLineIsBlank = true;
            }
            else if(c != '\r'){
              currentLineIsBlank = false;
            }
          }
        }
        delay(1);
        readString = "";
        client.stop();
        Serial.print("client is stoped");
      }
    }
