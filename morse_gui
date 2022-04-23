from tkinter import *
from gpiozero import LED
import RPi.GPIO
import time
RPi.GPIO.setmode(RPi.GPIO.BCM)
gui = Tk()
gui.title("LED control with text box")
gui.geometry("500x200")
led = LED(14)
# 0-ot, 1-dash
character = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z','0','1','2','3','4','5','6','7','8','9']
code = ['01','1000','1010','100','0','0010','110','0000','00','0111','101','0100','11','10','111','0110','1101','010','000','1','001','0001','011','1001','1011','1100','11111','01111','00111','00011','00001','00000','10000','11000','11100','11110']
morse_dict = dict(zip(character,code))

LIMIT_LENGTH = 12
led_text = StringVar()

def dash():
    led.blink(on_time = 1, off_time = 0.5, n = 1, background = False)
    
def dot():
    led.blink(on_time = 0.2, off_time = 0.5,n = 1, background = False)
    
def blink_led():
    for char in led_text.get().upper():
        code = morse_dict[char]
        for c in code:
            if c == "1":
                dash()
            else:
                dot()
        print(1)
        time.sleep(0.5)
    
def close():
    RPi.GPIO.cleanup()
    gui.destroy()

led_button = Button(gui, text = "Blink Morse Code",command = blink_led,bg = "bisque2",height =5, width = 15)
led_button.grid(row=0,column = 1)
#funciton to limit text length
def limit_text_size(*args):
    word = led_text.get()
    if len(word) > LIMIT_LENGTH:
        led_text.set(word[:LIMIT_LENGTH])
        
led_text.trace('w',limit_text_size)

text = Entry(gui, width = 15, textvariable = led_text)
text.grid(row = 0, column = 0)

gui.protocol("WM_DELETE_WINDOW",close)
gui.mainloop()
