# Zxing
Zxing横竖屏切换只需要修改
1、竖屏在DecodeHandler类中加上下面这段代码，横屏注释掉这段代码
byte[] rotatedData = new byte[data.length];
    for (int y = 0; y < height; y++) {
        for (int x = 0; x < width; x++)
            rotatedData[x * height + height - y - 1] = data[x + y * width];
    }
    int tmp = width; // Here we are swapping, that's the difference to #11
    width = height;
    height = tmp;
2、然后修改CameraManager中的下面这段代码
  竖屏为：
      rect.left = rect.left * cameraResolution.y / screenResolution.x;
      rect.right = rect.right * cameraResolution.y / screenResolution.x;
      rect.top = rect.top * cameraResolution.x / screenResolution.y;
      rect.bottom = rect.bottom * cameraResolution.x / screenResolution.y;
  横屏为：
      rect.left = rect.left * cameraResolution.x / screenResolution.x;
      rect.right = rect.right * cameraResolution.x / screenResolution.x;
      rect.top = rect.top * cameraResolution.y / screenResolution.y;
      rect.bottom = rect.bottom * cameraResolution.y / screenResolution.y;
3、修改AndroidManifest中的activity属性
      android:screenOrientation="xxxxx"
      portrait为竖屏，landscape为横屏
4、最后修改CameraConfigurationManager类中的这行代码
      setDisplayOrientation(camera, 90);  //90为竖屏，0为横屏
