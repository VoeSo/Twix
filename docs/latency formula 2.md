Formula that combines PresentMon data, refresh rate and polling rate to simulate input age for each frame in a trace.

https://www.nvidia.com/content/dam/en-zz/Solutions/geforce/news/reflex-low-latency-platform/nvidia-reflex-end-to-end-systeme-latency-pipline.png

Gives latency from start of "USB HW" to start of "Scanout". Display latency and mouse "HW" latency can be added manually to give end to end latency.


Formula:

(((((firstTimeInSeconds+((ROUNDUP((TimeInSeconds+(MsUntilDisplayed/1000)-firstTimeInSeconds)/(1/RefreshRate),0))*(1/RefreshRate)))-(TimeInSeconds+(MsUntilDisplayed/1000)))+((MsBetweenPresents/1000)+(MsUntilDisplayed/1000)-((prevMsInPresentAPI+SimSamp)/1000))+((prevTimeInSeconds+((prevMsInPresentAPI+SimSamp)/1000))-(((ROUNDDOWN((prevTimeInSeconds+((prevMsInPresentAPI+SimSamp)/1000)-firstTimeInSeconds)/(1/PollingRate),0))*(1/PollingRate))+firstTimeInSeconds)))+((1/PollingRate)/2))*1000)+DisplayLat+MouseHW+USBSW


RefreshRate....monitor refreshrate in Hz

PollingRate....USB pollingrate in Hz

firstTimeInSeconds....TimeInSeconds of the first frame in the benchmark

prevMsInPresentAPI....MsInPresentAPI of the previous frame

prevTimeInSeconds....TimeInSeconds of the previous frame

prevMsInPresentAPI....MsInPresentAPI of the previous frame

ROUNDUP(result,0)....Roundup the result of () to zero decimals

ROUNDDOWN(result,0)....Rounddown the result of () to zero decimals

SimSamp....time between simulation start and sampling in milliseconds

DisplayLat....latency from start of scannout until complete pixel transition in milliseconds

MouseHW....first part of mouse latency in milliseconds. Includes things like debounce, smoothing and varies depending on movement speed, dpi, sensor framerate, etc.

USBSW....USB packet processing latency in milliseconds. Includes interrupt latency, processing by csrss etc.

All other definitions can be found here https://github.com/GameTechDev/PresentMon


Excel formula to use on FrameView csv:

=((((($M$2+((ROUNDUP((M3+(R3/1000)-$M$2)/(1/$DI$2),0))*(1/$DI$2)))-(M3+(R3/1000)))+((N3/1000)+(R3/1000)-((P2+$DN$2)/1000))+((M2+((P2+$DN$2)/1000))-(((ROUNDDOWN((M2+((P2+$DN$2)/1000)-$M$2)/(1/$DJ$2),0))*(1/$DJ$2))+$M$2)))+((1/$DJ$2)/2))*1000)+$DK$2+$DL$2+$DM$2


Instructions:

1) Open a FrameView benchmark and put your refresh rate(hz) into the cell DI2, and then your polling rate(hz) into DJ2

2) Chose any cell in Row number 3(an empty cell is recommended) and copy paste the formula above into the cell

3) Use autofill to drag the formula to the bottom of your benchmark

4) You now have latency per frame, in milliseconds


Optional:

-Set Display latency in cell DK2

-Set Mouse "HW" latency in cell DL2

-Set "USB SW" latency in cell DM2


Caveats:

Works for dx11(and bellow, probably) but not for dx12.

Doesn't work with most frame limiters.

Doesn't work in severly GPU capped scenarios.

No PCL needed.

Made for fixed refresh rate, vsync disabled.
