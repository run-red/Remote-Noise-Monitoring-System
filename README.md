#Remote-Noise-Monitoring-System
#==============================

#A remote noise monitoring system, accessible over the internet

from tkinter import *
import serial


root = Tk()#initialise window
root.geometry('+200+200')#Window size and position
root.title('NL-52 Serial Console')#Window title


#Find available serial ports and append to OptionMenu
def scan():
    # scan for available ports. return a list of tuples (num, name)
   available = []
   for i in range(256):
       try:
           s = serial.Serial(i)
           available.append( (i, s.portstr))
           s.close()
       except serial.SerialException:
           pass
   return available

print ("Found ports:")
for n,s in scan(): print ("(%d) %s" % (n,s))

COMS = scan()#Assigning available ports to COMS variable


#Class 1

class App:

    def __init__(self, master):

        #Title Label
        title = Label(text="Select Settings").pack()
        
        #Separating line
        separator = Frame(height=2, bd=1, relief=SUNKEN)
        frame = Frame(master)

        #Option Menu, serial port selection
        com_variable = StringVar(frame)
        com_variable.set(COMS[0])
        self.com_select = OptionMenu(frame, com_variable, *COMS)

        #Buttons
        self.light_on = Button(frame, text="On", command = self.say_light_on)      #Backlight on
        self.light_off = Button(frame, text="Off", command = self.say_light_off)   #Backlight off
        self.set_eng = Button(frame, text="English", command = self.say_set_eng)   #Set English
        self.set_jap = Button(frame, text="Japanese", command = self.say_set_jap)  #Set Japanese
        self.lcd_on = Button(frame, text="On", command = self.say_lcd_on)          #LCD on
        self.lcd_off = Button(frame, text="Off", command = self.say_lcd_off)       #LCD off
        self.set_A = Button(frame, text="A", command = self.say_set_A)             #Set A-weighting
        self.set_C = Button(frame, text="C", command = self.say_set_C)             #Set C-weighting
        self.set_Z = Button(frame, text="Z", command = self.say_set_Z)             #Set Z-weighting
        self.quit = Button(frame, text="QUIT", fg="red", command=frame.quit)       #QUIT
    
        #Labels
        com_label=Label(frame, text="Select Port").grid(row=0, column=1, sticky=W)
        light_label=Label(frame, text="Backlight").grid(row=1, column=1, sticky=W)
        lang_label=Label(frame, text="Language").grid(row=2, column=1, sticky=W)
        lcd_label=Label(frame, text="LCD").grid(row=3, column=1, sticky=W)
        weight_label=Label(frame, text="Frequency Weighting").grid(row=4, column=1, sticky=W)
      
        #Geometry Management
        separator.pack(fill=X, padx=5, pady=5)
        frame.pack()

        self.com_select.grid(row=0, column=2, sticky=W)                 #Serial port selection
        self.light_on.grid(row=1, column=2, padx=6, pady=6, sticky=W)   #Backlight on
        self.light_off.grid(row=1, column=3, padx=6, pady=6, sticky=W)  #Backlight off
        self.set_eng.grid(row=2, column=2, padx=6, pady=6, sticky=W)    #Set English
        self.set_jap.grid(row=2, column=3, padx=6, pady=6, sticky=W)    #Set Japanese
        self.lcd_on.grid(row=3, column=2, padx=6, pady=6, sticky=W)     #LCD on
        self.lcd_off.grid(row=3, column=3, padx=6, pady=6, sticky=W)    #LCD off
        self.set_A.grid(row=4, column=2, padx=6, pady=6, sticky=W)      #Set A-weighting
        self.set_C.grid(row=4, column=3, padx=6, pady=6, sticky=W)      #Set C-weighting
        self.set_Z.grid(row=4, column=4, padx=6, pady=6, sticky=W)      #Set Z-weighting
        self.quit.grid(row=6, column=2, pady=10, sticky=W)              #Quit

        
    def say_light_on(self):
        print ("Backlight On!")

    def say_light_off(self):
        print ("Backlight Off!")

    def say_set_eng(self):
        print ("Language Set To English!")

    def say_set_jap(self):
        print ("Language Set To Japanese!")

    def say_lcd_on(self):
        print ("LCD On!")

    def say_lcd_off(self):
        print ("LCD Off!")

    def say_set_A(self):
        print ("A-weighting Set!")

    def say_set_C(self):
        print ("C-weighting Set!")

    def say_set_Z(self):
        print ("Z-weighting Set!")
        

app = App(root)

root.mainloop()
root.destroy()
