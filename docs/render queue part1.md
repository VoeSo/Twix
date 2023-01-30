# Testing nvidia settings effects on render queue in dx11 games

## Nvidia settings to test:
Maximum pre-rendered frames(only accessible with profile inspector)

Reflex low latency(ingame setting)

Low latency mode(nvcpl)

Maximum frames allowed(profile inspector)

Virtual Reality pre-rendered frames(nvcpl)

Frame limiter(ingame/nvcpl/inspector etc)

## Test method:
1) Create gpu bottleneck

   -Force slowest P-state by setting PowerMizerEnable 1 and PowerMizerLevelAC 3 in registry
    
   -Use highest graphics settings in-game
2) Compare benchmarks with nvidia frameview


## Games tested:
Apex legends

Overwatch

Kovaak fpsaimtrainer


## Findings:

You can see effects of various settings by eyeing "Render queue depth" in the frameview csv files.

A cpu capped scenario will always have a value between 0 and 1.(bc gpu finishes rendering the previous frame before the cpu can finish work on the current frame)

![alt text](https://github.com/VoeSo/Twix/blob/main/pics/rqd1.png)

With a massive gpu cap(in my case I got my gpu to render 10 times slower than cpu) the render queue gets filled to the max.

![alt text](https://github.com/VoeSo/Twix/blob/main/pics/rqd2fr.png)

Not manipulating the queue(not using any of the tools mentioned above), the maximum number of prerendered frames is ~2!


Setting "Maximum pre-rendered frames", "Maximum frames allowed", "Virtual Reality pre-rendered frames" has no effect on render queue.

Setting them to the maximum still doesn't allow a render queue depth of more than ~2.

Setting all to lowest/1 also has no effect, -depending how slow the gpu renders the queue gets filled with up to 2 frames.


Reflex low latency delays CPU frame generation so that it finishes right when gpu finishes the previous frame, keeping the queue close to 1.

![alt text](https://github.com/VoeSo/Twix/blob/main/pics/rqd1exactfr.png)


Low latency mode set to Ultra acts similar to reflex, keeping queue at 1.

Low latency mode set to On, has no effect, -queue can get filled up to 2.

(Low lateny mode set to Off has no effect)



Framelimiter, as long as the limit is actually hit, keeps queue close to 1.



To sum up, if you want to keep your render queue low in gpu capped scenarios, use either reflex, llm ultra or a framecap.

All other methods did not work in dx11 for multiple games but they might work with older games, ogl games etc.

[Beware, Reflex and llm functionality can break very easily](https://github.com/VoeSo/Twix/blob/main/docs/reflex%20llm%20bug)
