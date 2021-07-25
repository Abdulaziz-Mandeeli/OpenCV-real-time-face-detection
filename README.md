# OpenCV-real-time-face-detection
المهمة الرابعة لتدريب الاساليب الذكية

اولا:

نعمل تنزيل وتهيئة للملفات الازمة باستعمال الاكواد:

	import cv2
	faceCascade = cv2.CascadeClassifier('Cascades/haarcascades/HAARCASCADE_FRONTALFACE_DEFAULT.xml')
	eye_cascade = cv2.CascadeClassifier('Cascades/haarcascades/HAARCASCADE_EYE.xml')
	smileCascade = cv2.CascadeClassifier('Cascades/haarcascades/HAARCASCADE_SMILE.xml')

وبعدها نهيأ الكاميرا باستعمال الاكواد :

	cap = cv2.VideoCapture(0)
	cap.set(3,640) # set Width
	cap.set(4,480) # set Height

ثانيا :

نعمل استدعاء للفانكشن التالية باستعمال الكود

	while True:
   	 ret, img = cap.read()
   	 gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
   	 faces = faceCascade.detectMultiScale( gray, scaleFactor=1.2, minNeighbors=5, minSize=(20, 20) )

ثالثا:

لتمييز الوجوه نستعمل الكود

	for (x,y,w,h) in faces:
   	 cv2.rectangle(img,(x,y),(x+w,y+h),(255,0,0),2)
   	 roi_gray = gray[y:y+h, x:x+w]
   	 roi_color = img[y:y+h, x:x+w]

ولتمييز الاعين نستعمل الكود

   	for (ex, ey, ew, eh) in eyes:
        cv2.rectangle(roi_color, (ex, ey), (ex + ew, ey + eh), (0, 255, 0), 2)

وايضا لتمييز الابتسامة نستعمل الكود

    smile = smileCascade.detectMultiScale(roi_gray,scaleFactor=1.5,minNeighbors=15, minSize=(25, 25))
    for (xx, yy, ww, hh) in smile:
        cv2.rectangle(roi_color, (xx, yy), (xx + ww, yy + hh), (0, 255, 0), 2)

