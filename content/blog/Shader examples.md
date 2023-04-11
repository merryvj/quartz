
### Rectangle
https://www.youtube.com/watch?v=bigjgiavOM0&ab_channel=TheArtofCode

```

float Band(float t, float start, float end, float blur) {
    float step1 = smoothstep(start-blur, start+blur, t);
    float step2 = smoothstep(end+blur, end-blur, t);
    return step1*step2;
}

float Rect(vec2 uv, float left, float right, float bottom, float top, float blur) {
    float band1 = Band(uv.x, left, right, blur);
    float band2 = Band(uv.y, bottom, top, blur);
    return band1*band2;
}


void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    vec2 uv = fragCoord/iResolution.xy;
    uv -= .5;
    uv.x *= iResolution.x/iResolution.y;
    vec3 col = vec3(0.);
 
    
    float mask = Rect(vec2(x,y), -.5, .5, -.1, .1, 0.01);
    col = vec3(1.,1.,1.)*mask;
    
    fragColor = vec4(col, 1.);
 
    
}
```

Make it distorted!

https://www.youtube.com/watch?v=jKuXA0trQPE&ab_channel=TheArtofCode

```

float Band(float t, float start, float end, float blur) {
    float step1 = smoothstep(start-blur, start+blur, t);
    float step2 = smoothstep(end+blur, end-blur, t);
    return step1*step2;
}

float Rect(vec2 uv, float left, float right, float bottom, float top, float blur) {
    float band1 = Band(uv.x, left, right, blur);
    float band2 = Band(uv.y, bottom, top, blur);
    return band1*band2;
}


void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    vec2 uv = fragCoord/iResolution.xy;
    uv -= .5;
    uv.x *= iResolution.x/iResolution.y;
    vec3 col = vec3(0.);
    
    float x = uv.x;
    
    float m = (sin(iTime + x*1.)*sin(iTime + x*10.)) * .1;
    float y = uv.y - m;
    
    
    float mask = Rect(vec2(x,y), -1., 1., -.01, .01, 0.01);
    col = vec3(1.,1.,1.)*mask;
    
    fragColor = vec4(col, 1.);
 
    
}

```
