pip install opencv-python

import cv2
import numpy as np

# Create a blank canvas (white image)
canvas = np.ones((400, 400, 3), dtype=np.uint8) * 255

# Initialize brush settings
brush_color = (0, 0, 255)  # Red color (BGR format)
brush_size = 5

# Initialize drawing state
drawing = False
prev_point = None

# Mouse callback function
def draw(event, x, y, flags, param):
    global canvas, prev_point, drawing

    if event == cv2.EVENT_LBUTTONDOWN:
        drawing = True
        prev_point = (x, y)
    elif event == cv2.EVENT_MOUSEMOVE:
        if drawing:
            cv2.line(canvas, prev_point, (x, y), brush_color, brush_size)
            prev_point = (x, y)
    elif event == cv2.EVENT_LBUTTONUP:
        drawing = False

# Create a window and set the mouse callback function
cv2.namedWindow("AI Brush Tool")
cv2.setMouseCallback("AI Brush Tool", draw)

while True:
    cv2.imshow("AI Brush Tool", canvas)

    # Press 'q' to quit
    if cv2.waitKey(1) & 0xFF == ord("q"):
        break

cv2.destroyAllWindows()
