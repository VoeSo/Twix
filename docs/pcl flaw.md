I think PCL is inherintely flawed and it seems that it's just assuming a gpu capped scenario with filled render queue by default.

![alt text](https://github.com/VoeSo/Twix/blob/main/pics/pcl_bug.png)

frametimes are stable around 4ms whatever and pcl is stable as well

Then 1 frame takes longer with 14ms and look what PCL does

the next two frames get higher latency even though frametime is normal again

Happens for every trace I checked so far

Look at 3 last rows it happens again

