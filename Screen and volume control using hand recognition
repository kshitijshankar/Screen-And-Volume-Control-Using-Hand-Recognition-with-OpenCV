Import	cv2
from	cvzone.HandTrackingModule	import	HandDetector
import	pyautogui
from	ctypes	import	cast,	POINTER
from	comtypes	import	CLSCTX_ALL
import	mediapipe	as	mp
import	tensorflow	as	tf
from	tensorflow.keras.models	import	load_model
from	pycaw.pycaw	import	AudioUtilities,	IAudioEndpointVolume
import	screen_brightness_control	as	sbc
import	numpy	as	np
devices	=	AudioUtilities.GetSpeakers()
interface	=	devices.Activate(IAudioEndpointVolume.iid,	CLSCTX_ALL,	None)
volume=cast(interface,POINTER(IAudioEndpointVolume))
volRange=	volume.GetVolumeRange()
minvol=volRange[0]
maxvol=volRange[1]
vol=0
volBar=0
bright=0
brightbar=0
cap=cv2.VideoCapture(0)
detector=	HandDetector(detectionCon=0.8)
gesture=""
while	True:
				success,img=cap.read()
				hands,img=detector.findHands(img)
				if	hands:
								hand1=hands[0]
								lmList1=hand1["lmList"]
								bbox1=hand1["bbox"]
								centerPoint1=hand1["center"]
								handType1=hand1["type"]
								
								print(handType1)
								
								if(handType1=="Right"):
												length,info,img=detector.findDistance(lmList1[4],lmList1[8],img)
												finger1=detector.fingersUp(hand1)
												print(finger1)
												
												
												if(finger1[0]==1	and	finger1[1]==1	and	finger1[2]==1	and	finger1[3]==1	and	finger1[4]==1):
																
																if(gesture=="OPEN	HAND"):
																				pyautogui.hotkey('playpause')
																				pyautogui.PAUSE=1
																gesture="OPEN	HAND"
																
												elif(finger1[0]==0	and	finger1[1]==0	and	finger1[2]==0	and	finger1[3]==0	and	finger1[4]==0):
																print("CLOSED	HAND")
																if(gesture=="CLOSED	HAND"):
																				pyautogui.hotkey('alt','f4')
																				pyautogui.PAUSE=1
																gesture="CLOSED	HAND"
																
												elif(finger1[0]==1	and	finger1[1]==1	and	finger1[2]==0	and	finger1[3]==0	and	finger1[4]==0):
																print("THUMBS	UP")
																if(gesture=="SEVEN"):
																				pyautogui.hotkey('ctrl','tab')
																				pyautogui.PAUSE=1
																gesture="SEVEN"
																
												elif(finger1[0]==0	and	finger1[1]==1	and	finger1[2]==0	and	finger1[3]==0	and	finger1[4]==0):
																print("ONE")
																if(gesture=="ONE"):
																				pyautogui.hotkey('up')
																gesture="ONE"
																
												elif(finger1[0]==0	and	finger1[1]==1	and	finger1[2]==1	and	finger1[3]==0	and	finger1[4]==0):
																print("TWO")
																if(gesture=="TWO"):
																				pyautogui.hotkey('down')
																gesture="TWO"
																
												elif(finger1[0]==0	and	finger1[1]==0	and	finger1[2]==1	and	finger1[3]==1	and	finger1[4]==1):
																print("OKAY")
																if(gesture=="OKAY"):
																				pyautogui.hotkey('win','prtsc')
																				pyautogui.PAUSE=1
																gesture="OKAY"
																
								if(handType1=="Left"):
												length,info,img=detector.findDistance(lmList1[4],lmList1[8],img)
												vol=np.interp(length,[15,220],[minvol,maxvol])
												volBar=np.interp(length,[50,300],[400,150])
												print(vol,length)
												volume.SetMasterVolumeLevel(vol,	None)
				cv2.rectangle(img,(50,150),(85,400),(0,255,0),3)
				cv2.rectangle(img,(50,int(volBar)),(85,400),(255,0,0),cv2.FILLED)
				cv2.imshow("IMAGE	TEST",img)
				key_pressed=cv2.waitKey(1)	&	0xFF
				if	key_pressed	==	ord('q'):
								break;
cap.release()
cv2.destroyAllWindows()
print("1")
