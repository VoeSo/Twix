Testing reflex and breaking it


Force gpu limited scenario with powermizer


[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\****\0000] Replace **** with device class guid (device manger -> gpu -> properties -> details -> device class guid)

"PowerMizerEnable"=dword:00000001

"PowerMizerLevelAC"=dword:00000003


Launch reflex supported game, enable reflex and run a quick frameview benchmark.

Open the csv and look at Render queue depth...if reflex works it will be around 1.


Things that break reflex for me(1080ti/456.71):

Shaddow settings(Dynamic spot shadows in apex; shadows in kovaak; shadow detail in ow2)

Changing frl1 in inspector (Setting ID_0x10834fee)

Nvidia sharpening (only in ow2 so far)


Weird PCL thing:

Compare frameview PCL numbers

1) reflex disabled

2) reflex enabled

3) reflex enabled but broken


For me there is dramatic change between disabled and enabled, but even after breaking there is still a decent reduction in PCL when toggling on broken reflex.

IMO pcl assumes a full render queue by default, resulting in higher latency numbers and then assumes a more empty queue when reflex is toggled on.





