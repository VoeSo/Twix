A latency simulation formula, based on refresh rate, polling rate and PresentMon frame data.

Simulates latency from USB interrupt to Monitor refresh. Excludes the latency from Windows processing the mouse data(varies between systems), excludes monitor latency(pixel response time etc.) and mouse latency(click to interrupt). 


Formula:

(((firstTimeInSeconds+((ROUNDUP((TimeInSeconds+(MsUntilDisplayed/1000)-firstTimeInSeconds)/(1/RefreshRate),0))*(1/RefreshRate)))-(TimeInSeconds+(MsUntilDisplayed/1000)))+((MsBetweenPresents/1000)+(MsUntilDisplayed/1000)-(prevMsInPresentAPI/1000))+((prevTimeInSeconds+(prevMsInPresentAPI/1000))-(((ROUNDDOWN((prevTimeInSeconds+(prevMsInPresentAPI/1000)-firstTimeInSeconds)/(1/PollingRate),0))*(1/PollingRate))+firstTimeInSeconds)))*1000


RefreshRate....monitor refreshrate in Hz

PollingRate....USB pollingrate in Hz

firstTimeInSeconds....TimeInSeconds of the first frame in the benchmark

prevMsInPresentAPI....MsInPresentAPI of the previous frame

prevTimeInSeconds....TimeInSeconds of the previous frame

prevMsInPresentAPI....MsInPresentAPI of the previous frame

ROUNDUP(result,0)....Roundup the result of () to zero decimals

ROUNDDOWN(result,0)....Rounddown the result of () to zero decimals


Excel formular to use on FrameView csv:

=((($M$2+((ROUNDUP((M3+(R3/1000)-$M$2)/(1/$DI$2),0))*(1/$DI$2)))-(M3+(R3/1000)))+((N3/1000)+(R3/1000)-(P2/1000))+((M2+(P2/1000))-(((ROUNDDOWN((M2+(P2/1000)-$M$2)/(1/$DJ$2),0))*(1/$DJ$2))+$M$2)))*1000


Instructions:

1) Open a FrameView benchmark and put your refresh rate(hz) into the cell DI2, and then your polling rate(hz) into DJ2

2) Chose any cell in Row number 3(an empty cell is recommended) and copy paste the formula above into the cell

3) Use autofill to drag the formula to the bottom of your benchmark
