import smbus2 
import time 
import RPi.GPIO as GPIO 
import smtplib 
from email.mime.multipart import MIMEMultipart 
from email.mime.text import MIMEText 
from email.mime.base import MIMEBase 
from email import encoders 
# === Email Configuration === 
fromaddr = "tdinesh986@gmail.com" 
toaddr = "priyatharsann7@gmail.com" 
def mail(text): 
print(text) 
msg = MIMEMultipart() 
msg['From'] = fromaddr 
msg['To'] = toaddr 
msg['Subject'] = "VEHICLE SAFETY SYSTEM" 
body = text 
msg.attach(MIMEText(body, 'plain')) 
30 
31 
 
    try: 
        filename = "output/img.jpg" 
        attachment = open(filename, "rb") 
        p = MIMEBase('application', 'octet-stream') 
        p.set_payload(attachment.read()) 
        encoders.encode_base64(p) 
        p.add_header('Content-Disposition',f"attachment; 
filename={filename}") 
        msg.attach(p) 
    except FileNotFoundError: 
        print("Image not found, continuing without attachment.") 
 
    s = smtplib.SMTP('smtp.gmail.com', 587) 
    s.starttls() 
    s.login(fromaddr, "alilgaievmduuxbb")  # App password 
    s.sendmail(fromaddr, toaddr, msg.as_string()) 
    s.quit() 
# === I2C LCD Constants === 
I2C_ADDR = 0x27 
LCD_WIDTH = 16 
LCD_CHR = 1 
LCD_CMD = 0 
LCD_LINE_1 = 0x80 
LCD_LINE_2 = 0xC0 
LCD_BACKLIGHT = 0x08 
ENABLE = 0b00000100 
# === GPIO Setup === 
VIBRATION_PIN = 17 
GPIO.setmode(GPIO.BCM) 
GPIO.setup(VIBRATION_PIN, GPIO.IN) 
bus = smbus2.SMBus(1) 
# === LCD Functions === 
def lcd_init(): 
lcd_write(0x33, LCD_CMD) 
lcd_write(0x32, LCD_CMD) 
lcd_write(0x06, LCD_CMD) 
lcd_write(0x0C, LCD_CMD) 
lcd_write(0x28, LCD_CMD) 
lcd_write(0x01, LCD_CMD) 
time.sleep(0.005) 
32 
33 
 
def lcd_write(bits, mode): 
    high = mode | (bits & 0xF0) | LCD_BACKLIGHT 
    low = mode | ((bits << 4) & 0xF0) | LCD_BACKLIGHT 
    bus.write_byte(I2C_ADDR, high) 
    lcd_toggle_enable(high) 
    bus.write_byte(I2C_ADDR, low) 
    lcd_toggle_enable(low) 
 
def lcd_toggle_enable(bits): 
    time.sleep(0.0005) 
    bus.write_byte(I2C_ADDR, (bits | ENABLE)) 
    time.sleep(0.0005) 
    bus.write_byte(I2C_ADDR, (bits & ~ENABLE)) 
    time.sleep(0.0005) 
 
def lcd_message(message, line): 
    message = message.ljust(LCD_WIDTH, " ") 
    lcd_write(line, LCD_CMD) 
    for char in message: 
        lcd_write(ord(char), LCD_CHR) 
34 
 
 
# === MAIN PROGRAM === 
try: 
    lcd_init() 
    lcd_message("System Init...", LCD_LINE_1) 
    lcd_message("Please Wait...", LCD_LINE_2) 
    time.sleep(2) 
    lcd_message("Check Vibration", LCD_LINE_1) 
    lcd_message("Location:Chennai", LCD_LINE_2) 
    time.sleep(3) 
    last_state = 0 
    chennai_location = "Lat:13.0827\nLon:80.2707 (Chennai)" 
    while True: 
        vibration = GPIO.input(VIBRATION_PIN) 
        lcd_message(f"Vib: {vibration}", LCD_LINE_1) 
        if vibration == 1 and last_state == 0: 
            lcd_message("VIBRATION DETECT", LCD_LINE_1) 
            lcd_message("Chennai Location", LCD_LINE_2) 
            mail("Vibration Detected at:\n" + chennai_location) 
            last_state = 1 
35 
 
        elif vibration == 0: 
            lcd_message("Monitoring...", LCD_LINE_1) 
            lcd_message("No Vibration", LCD_LINE_2) 
            last_state = 0 
        time.sleep(2) 
except KeyboardInterrupt: 
    lcd_message("System Halted", LCD_LINE_1) 
    GPIO.cleanup() 
