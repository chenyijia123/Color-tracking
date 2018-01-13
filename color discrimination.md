# Color-tracking
import sensor, image, time
green_threshold   = ( 30, 100, -70, -0, 10, 30)
red_threshold = ( 15, 50, 40, 80, 20, 60)
blue_threshold = ( 30, 50, 0, 20, -45, -20)
yellow_threshold = ( 65, 80, -10, 10, 60, 70)
green_number = 0
red_number = 0
blue_number = 0
yellow_number = 0
sensor.reset() # Initialize the camera sensor.
sensor.set_pixformat(sensor.RGB565) # use RGB565.
sensor.set_framesize(sensor.QQVGA) # use QQVGA for speed.
sensor.skip_frames(10) # Let new settings take affect.
sensor.set_auto_whitebal(False) # turn this off.
#关闭白平衡。白平衡是默认开启的，在颜色识别中，需要关闭白平衡。
clock = time.clock() # Tracks FPS.
while(True):
    clock.tick() # Track elapsed milliseconds between snapshots().
    img = sensor.snapshot() # Take a picture and return the image.
    green_blobs = img.find_blobs([green_threshold])
    if green_blobs:
        for b in green_blobs:
            img.draw_rectangle(b[0:4],color=(255,255,255))
            green_number = green_number + 1
    red_blobs = img.find_blobs([red_threshold])
    if red_blobs:
        for b in red_blobs:
            img.draw_rectangle(b[0:4],color=(255,255,255))
            red_number = red_number + 1
    blue_blobs = img.find_blobs([blue_threshold])
    if blue_blobs:
        for b in blue_blobs:
            img.draw_rectangle(b[0:4],color=(255,255,255))
            blue_number = blue_number + 1
    yellow_blobs= img.find_blobs([yellow_threshold])
    if yellow_blobs:
        for b in yellow_blobs:
            img.draw_rectangle(b[0:4],color=(255,255,255))
            yellow_number = yellow_number + 1
    print( green_number, red_number, blue_number, yellow_number)
    green_number = 0
    red_number = 0
    blue_number = 0
    yellow_number = 0
