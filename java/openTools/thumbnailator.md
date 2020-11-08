# Thumbnailator

<a name="McG3W"></a>
## 参考文档
[GitHub](https://github.com/coobird/thumbnailator)

- Java缩略图生成开源工具



<a name="og7oi"></a>
## 快速使用
```xml
<dependency>
  <groupId>net.coobird</groupId>
  <artifactId>thumbnailator</artifactId>
  <version>0.4.12</version>
</dependency>
```
```java

    /**
     * 自定义图片Filter
     * 解决透明背景会被设置为黑色背景问题（替换为白色背景）
     */
    public class ThumbnailsImgFilter implements ImageFilter {
        @Override
        public BufferedImage apply(BufferedImage img) {
            int wight = img.getWidth();
            int height = img.getHeight();
            BufferedImage newImage = new BufferedImage(wight, height, BufferedImage.TYPE_INT_RGB);
            Graphics2D graphic = newImage.createGraphics();
            graphic.setColor(Color.WHITE);
            graphic.fillRect(0, 0, wight, height);
            graphic.drawRenderedImage(img, null);
            graphic.dispose();
            return newImage;
        }
    }

    /**
     * 指定宽高创建缩略图
     * PNG等含透明背景的图,经过压缩后背景会变为黑色（解决方案通过设置Filter解决）
     */
    @Test
    public void changeSizeTest() {
        try {
            Thumbnails.of(new File(WATERMARK_IMAGE_PATH))
                    // call addFilter
                    .addFilter(new ThumbnailsImgFilter())
                    .size(160, 160)
                    .toFile(TARGET_IMAGE_PATH);
        } catch (IOException ioe) {
            LogUtils.error(LOGGER, ioe, "io is exception, errorMsg=", ioe.getMessage());
        }
    }

    /**
     * 指定比例创建缩略图
     */
    @Test
    public void changeScaleTest() {
        try {
            Thumbnails.of(new File(SRC_IMAGE_PATH))
                    // 设置比例
                    .scale(0.5)
                    // 设置输出格式（设置此值会覆盖目标文件的扩展名（如有）
                    .outputFormat("png")
                    .toFile(TARGET_IMAGE_PATH);
        } catch (IOException ioe) {
            LogUtils.error(LOGGER, ioe, "io is exception, errorMsg=", ioe.getMessage());
        }
    }

    /**
     * 添加水印到指定位置及透明度
     */
    @Test
    public void watermarkTest() {
        try {
            float opacity = 0.5f;
            Thumbnails.of(new File(SRC_IMAGE_PATH)).scale(0.75)
                    // 位置 水印源 透明度
                    .watermark(Positions.BOTTOM_RIGHT, ImageIO.read(new File(WATERMARK_IMAGE_PATH)), opacity)
                    // 设置压缩质量
                    .outputQuality(0.8)
                    .toFile(TARGET_IMAGE_PATH);
        } catch (IOException ioe) {
            LogUtils.error(LOGGER, ioe, "io is exception, errorMsg=", ioe.getMessage());
        }
    }

    /**
     * 图片旋转
     */
    @Test
    public void rotateTest() {
        try {
            double rotate = 90d;
            Thumbnails.of(SRC_IMAGE_PATH).scale(1)
                    // 旋转度数
                    .rotate(rotate)
                    .toFile(TARGET_IMAGE_PATH);
        } catch (IOException ioe) {
            LogUtils.error(LOGGER, ioe, "io is exception, errorMsg=", ioe.getMessage());
        }
    }

    /**
     * 图片裁剪
     */
    @Test
    public void regionTest() {
        try {
            Thumbnails.of(SRC_IMAGE_PATH).scale(1)
                    // 源图裁剪区间
                    .sourceRegion(Positions.CENTER, 100, 100)
                    .toFile(TARGET_IMAGE_PATH);
        } catch (IOException ioe) {
            LogUtils.error(LOGGER, ioe, "io is exception, errorMsg=", ioe.getMessage());
        }
    }

    /**
     * 批量处理
     */
    @Test
    public void batchScaleTest() {
        try {
            Thumbnails.of(SRC_IMAGE_PATH, SRC_IMAGE_PATH2, SRC_IMAGE_PATH3)
                    .scale(0.75)
                    // Rename.NO_CHANGE - 保持原名
                    .toFiles(new File(TARGET_IMAGE_PATH), Rename.PREFIX_DOT_THUMBNAIL);
        } catch (IOException ioe) {
            LogUtils.error(LOGGER, ioe, "io is exception, errorMsg=", ioe.getMessage());
        }
    }
```
