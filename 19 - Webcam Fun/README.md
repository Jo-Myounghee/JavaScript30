# 1. video.srcObject = localMediaStream;

처음에 코드는 

```javascript
video.src = window.URL.createObjectURL(localMediaStream);
```

이었는데, 자꾸 오류가 나서 

```javascript
video.srcObject = localMediaStream;
```

으로 바꿨는데 괜찮아졌다.