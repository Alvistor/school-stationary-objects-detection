# objects-detection school stationary items detection



import cv2
####################################
cameraNo = 0
objectName = 'PENCIL'
objectName1 = 'SHARPENER'



frameWidth = 640
frameHeight = 480
####################################

cap = cv2.VideoCapture(0)

cap.set(4, frameHeight)
cap.set(3, frameWidth)

pencil_cascade = cv2.CascadeClassifier('pencilcascade.xml')
sharpener_cascade = cv2.CascadeClassifier('sharpenercascade.xml')




while True:

    success, img = cap.read()
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    pencil = pencil_cascade.detectMultiScale(img, 1.30, 5)
    sharpener = sharpener_cascade.detectMultiScale(img, 1.3, 5)
    

    for (x, y, w, h) in pencil:

        cv2.rectangle(img, (x, y), (x + w, y + h), (255, 0, 0), 2)
        cv2.putText(img, objectName, (x, y - 5), cv2.FONT_HERSHEY_COMPLEX_SMALL, 1, (255, 0, 0), 2)
        roi_gray = gray[y:y + h, x:x + w]
        roi_color = img[y:y + h, x:x + w]
    for (ex, ey, ew, eh) in sharpener:
        cv2.rectangle(img, (ex, ey), (ex + ew, ey + eh), (0, 255, 0), 2)
        cv2.putText(img, objectName1, (ex, ey - 5), cv2.FONT_HERSHEY_COMPLEX_SMALL, 1, (0, 255, 0), 2)
    
    cv2.imshow("result", img)
    if cv2.waitKey(1) & 0XFF == ord('x'):
        break
cv2.destroyAllWindows()


