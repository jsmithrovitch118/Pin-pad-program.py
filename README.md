import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)

inputs = [12,25,24,23]
outputs = [16,20,21]

GPIO.setup(inputs, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)
GPIO.setup(outputs, GPIO.OUT)

r1 = ["1", "2", "3"]
r2 = ["4", "5", "6"]
r3 = ["7", "8", "9"]
r4 = ["*", "0", "#"]


def check():
    row = 0
    if GPIO.input(12) == True:
        row = r1
    elif GPIO.input(25) == True:
        row = r2
    elif GPIO.input(24) == True:
        row = r3
    elif GPIO.input(23) == True:
        row = r4
    if row != 0:
        selection = row[col]
        print("the key pressed was " + selection)
        time.sleep(0.3)
        if selection == "#":
            global end
            end = 1
            
end = 0

while end == 0:
    GPIO.output(21,GPIO.HIGH)
    col = 0
    check()
    GPIO.output(21,GPIO.LOW)
    GPIO.output(20,GPIO.HIGH)
    col = 1
    check()
    GPIO.output(20,GPIO.LOW)
    GPIO.output(16,GPIO.HIGH)
    col = 2
    check()
    GPIO.output(16, GPIO.LOW)
    
GPIO.cleanup()
    
    
