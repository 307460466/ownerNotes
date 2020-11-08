# IText
### 99.FAQ
#### 1）Html转PDF，html强制换行样式未生效问题
- 强制换行样式：word-break: break-all;
- 基于IText7
```java
Document document = new Document(pdfDocument, PageSize.A4.rotate());
try {
    //设置页面边距 必须先设置边距，再添加内容，否则页边距无效
    document.setMargins(20, 20, 20, 20);
    List<IElement> list = HtmlConverter.convertToElements(htmlStr, converterProperties);
    //解决word-break: break-all;不兼容的问题
    document.setProperty(Property.SPLIT_CHARACTERS,new DefaultSplitCharacters(){
        @Override
        public boolean isSplitCharacter(GlyphLine text, int glyphPos) {
            return true;
        }
    });
    for (IElement ie : list) {
        document.add((IBlockElement) ie);
    }
} catch (Exception e) {
    LogUtil.error(LOGGER, e, "生成PDF失败");
    throw new RuntimeException("生成PDF失败", e);
} finally {
    document.close();
}
```