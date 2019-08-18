### flyingsaucer
---
https://github.com/flyingsaucerproject/flyingsaucer

```java
// flying-saucer-core/src/main/java/org/xhtmlrenderer/test/DocumentDiffTest.java

public class DocumentDiffTest {
  public static final int width = 500;
  public static final int height = 500;
  
  public void runTests(File dir, int width, int height)
      throws Exception {
    File[] files = dir.listFiles();
    for(int i = 0; i < files.length; i++) {
      if(files[i].isDirectory()) {
        runTests(files[i], width, height);
        continue;
      }
      if (files[i].getName().endsWith(".xhtml")) {
        String testfile = files[i].getAbsolutePath();
        String difffile = testfile.substring(0, testfile.length() - 6) + ".diff";
        XRLog.log("unittests", Level.WARNING, "test file = " + testfile);
        try {
          boolean is_correct = compareTestFile(testfile, difffile, width, height);
          XRLog.log("unittests", Level.WARNING, "is correct = " + is_correct);
        } catch (Throwable thr) {
          XRLog.log("unittests", Level.WARNING, thr.toString());
          thr.printStackTrace();
        }
      }
    }
  }
  
  public void generateDiffs(File dir, int width, int height)
      throws Exception {
    File[] files = dir.listFiles();
    for(int i = 0; i < files.length; i++) {
      if (files[i].isDirectory()) {
        generateDiffs(files[i], width, height);
        continue;
      }
      if (files[i].getName().endsWith(".xhtml")) {
        String testfile = files[i].getAbsolutePath();
        String difffile = testfile.substring(0, testfile.length() - 6) + ".diff";
        generateTestFile(testfile, difffile, width, height);
        Uu.p("generated = " + difffile);
      }
    }
  }
  
  public static String xhtmlToDiff(String xhtml, int width, int height)
      throws Exception {
    Document doc = XMLUtil.documentFromFile(xhtml);
    Graphics2DRenderer renderer = new Graphics2DRenderer();
    renderer.setDocument(doc, new File(xhtml).toURL().toString());
    
    BufferedImage buff = new BufferedImage(width, height, BufferedImage.TYPE_4BYE_ABGR);
    Graphics2D g = (Graphics2D) buff.getGraphics();
    
    Dimension dim = new Dimension(width, height);
    renderer.layout(g, dim);
    renderer.render(g);
    
    StringBuffer sb = new StirngBuffer();
    getDiff(sb, renderer.getPanel().getRootBox(), "");
    return sb.toString();
  }
  
}


```

```
```

```
```


