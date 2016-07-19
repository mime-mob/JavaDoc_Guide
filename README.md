#版权信息配置
>File -> settings -> Editor -> Copyright -> Copyright Profiles

![添加版权文件](https://github.com/mime-mob/JavaDoc_Guide/blob/master/img/pic.png)
</br>添加一个版本信息文件；右侧会出现默认的copyright信息，如名称（添加时输入的名称）、版权内容、在注释中添加版权信息的关键字等。</br>
![版权文件信息](https://github.com/mime-mob/JavaDoc_Guide/blob/master/img/pic2.png)
</br>这里，我们主要修改版本内容；具体内容略。修改完成后点击“Validate”按钮。
</br>
添加完成后，还需要设置一下，才能将版权信息添加到文件中。
</br>1. 在Settings中左侧选中Copyright，然后在右侧的下拉选择中选择刚刚添加的copyright。</br>
![配置copyright](https://github.com/mime-mob/JavaDoc_Guide/blob/master/img/pic3.png)
</br>2. 选中后，点击 + 号，然后选择ALL</br>
![添加ALL](https://github.com/mime-mob/JavaDoc_Guide/blob/master/img/pic4.png)
</br>
以上
</br>
##类说明及作者
	file -> settings -> Editor -> File and Code Templates
</br>右侧选择  **Includes**  然后选择 **File Header**
![这里写图片描述](https://github.com/mime-mob/JavaDoc_Guide/blob/master/img/pic5.png)
</br>内置的变量：</br>
**\${PACKAGE_NAME}** 文件所在的包名</br>
**\${USER}** 当前系统的登录名</br>
**\${DATE}** 当前系统日期</br>
**\${TIME}** 当前系统的时间</br>
**\${YEAR}** 当前系统的年份</br>
**\${MONTH}** 当前系统的月份</br>
**\${MONTH_NAME_SHORT}** 当前月份的名称缩写：Jan, Feb等等</br>
**\${MONTH_NAME_FULL}** 当前月份名称的全称： January，February等等</br>
**\${DAY}** 当前月的天，几号</br>
**\${HOUR}** 当前的小时</br>
**\${MINUTE}** 当前的分钟</br>
**\${PROJECT_NAME}** 当前的工程名</br>

#Javadoc

首先来看下Android Studio默认生成的DOC样式：
```
public class Sample {
    /**
     * This is a method description that is long enough to exceed right margin.
     * <p/>
     * Another paragraph of the description placed after blank line.
     * <p/>
     * Line with manual
     * line feed.
     *
     * @param i                  short named parameter description
     * @param longParameterName  long named parameter description
     * @param missingDescription
     * @return return description.
     * @throws XXXException description.
     * @throws YException   description.
     * @throws ZException
     * @invalidTag
     */
    public abstract String sampleMethod(int i, int longParameterName, int missingDescription) throws XXXException, YException, ZException;

    /**
     * One-line comment
     */
    public abstract String sampleMethod2();

    /**
     * Simple method description
     *
     * @return
     */
    public abstract String sampleMethod3();
```
如上面代码片段，doc文档通常用 /\*\*...*/ 注释块包裹起来的。</br>
javadoc文档包含三个部分：</br>
1. 简述。通常文档的第一句都是高度概括性的语句；对所描述对象是一个简洁而又完整的介绍。第一句都是以一个句号结尾，然后跟一个空格、TAB、换行符等等，亦可以直接跟一个HTML的标签(&nbsp, \<\!---->)然后直接跟接下来的部分。</br>
2. 详细的说明部分。要求对所描述的对象进行尽可能详细的说明，并指明各个依赖关系，使用的平台，定义清楚哪些是使用该类或方法所必要的条件，边界条件，存在的缺陷等。理想的情况下，其他人员通过对这部分的阅读就可以了解代码的实现，从而能够写出一个实质性的测试用例。这个部分没有严格的格式要求，可以有多个语句。通常以段落或者列表的方式描述，通过HTML的标签来分段，分行。这一部分与第一部分没有明显的分段，分行的区分，在文档格式上可以放在一起。</br>
3. 特殊部分的说明。这部分主要是对参数，版本信息，返回值等进行说明。</br>

##Javadoc的标签
###doc标签
> @author 标明开发该类模块的作者，可以多次使用来指明多个作者</br>
@version 标明该类模块的版本</br>
@param 方法中某个参数的说明</br>
@return 方法中返回值的说明</br>
@exception 对方法可能抛出的异常进行说明，@throws也是一样的</br>
@see 参考转向，也就是相关 主题</br>
@since 标明方法、类可运行的版本号</br>
@serial（或者是@serialField或者是@serialData）某个系列？</br>
@deprecated 表示已经废弃的方法</br>

###标签顺序
当有多个标签时，标签的顺序跟上述顺序是一样的。但是如果同一个标签出现了不止一次的话。可以分组标签，比如说多个@see标签，可以将所有的标签写在一起，每个标签单独一行。
</br>多个@author标签的话，以时间顺序，罗列在最开始的地方
</br>多个@param标签的话，按照参数的顺序。使得在视觉上跟声明的顺序更加匹配。
</br>多个@throws标签的话，按照字母的顺序罗列。
</br>多个@see标签的话，就如同下面展示的；跟文档中的顺序大致相同。方法的排序根据参数的数量排序。如果需要第二种排序依据的话，就按照字母的顺序排序
```
@see #field
@see #Constructor(Type, Type...)
@see #Constructor(Type id, Type id...)
@see #method(Type, Type,...)
@see #method(Type id, Type, id...)
@see Class
@see Class#field
@see Class#Constructor(Type, Type...)
@see Class#Constructor(Type id, Type id)
@see Class#method(Type, Type,...)
@see Class#method(Type id, Type id,...)
@see package.Class
@see package.Class#field
@see package.Class#Constructor(Type, Type...)
@see package.Class#Constructor(Type id, Type id)
@see package.Class#method(Type, Type,...)
@see package.Class#method(Type id, Type, id)
@see package
```
###便签说明风格
@param： 一个空格然后跟参数的变量名字，之后空格跟对该参数的描述</br>
@return： 如果返回为空的话可以省略，如果返回值就是参数值，必须用与参数值一致的描述</br>
@throws：函数所抛异常，需要说明抛异常的情况</br>
@deprecated 说明废弃原因，以及替代方法如果有的话</br>
###变量
{@inheritDoc} 从复写方法中拷贝出来的描述</br>
{@link reference} 链接到其他的引用</br>
{@Value} 返回一个静态作用域值</br>


##风格说明
###使用在关键词或者名称上添加`<code>...</code>` 样式 
</br>关键词包括：</br>
>Java关键字 | 包名 | 类名 | 方法名 | 接口名 | 属性名 | 参数名 | 代码示例

###合理使用内链
对API的名称上添加{@link}的便签是被鼓励的行为，但是也没有必要在doc的文档里给每个API的名字上都添加上这个链接便签。因为链接会修改自身的颜色，下划线，在源代码中的注释中的长度来引起注意，如果大量使用的话反而会引起阅读时困难。在哪些情况下使用链接呢？</br>
- 你认为使用者在想要看到更多信息的时候
- 当API名称第一次出现在文档中的时候。不要重复用同一个链接
</br>因为我们的读者都是程序员，因此并不是所有的API都需要添加连接的，java.lang中的API或者其他众所周知的方法都不需要添加。

###可以为一般的方法或者构造方法省略括号	
当你在写javadoc文档的时候需要指明一个方法或者构造函数有多个形式，如果你需要具体指明某一个确切的方法的话，那么就要使用括号和参数类型。

###使用短语代替完整的句子也是可以的
特别是在做初步总结和param标记做描述的时候。

###使用第三人称的描述而不是第二人称的规定
举个例子：
</br>Gets the label. （推荐）
</br>Get the label. （避免）
###方法的描述以动词短语开始
方法一般是实现一个操作，因此通常是以动词短语开始。
</br>举个例子：
</br>Gets the label of the button.（推荐）
</br>this method gets the label of this button(避免)
###类，接口，属性描述可以省略主题或所陈述的对象
这些API通过是描述物件而非动作行为。
</br>举个例子：
</br>A button label.（推荐）
</br>This field is a button label. （避免）
###当指向一个当前类创建的对象时，使用 this 代替 the。
举个例子：API  getToolkit 方法的描述应该是：
</br>Gets the toolkit for this component. （推荐）
</br>Gets the toolkit for the component. （避免）
###添加超过API名称的描述
好的API的名称能够告诉你这个API是做什么的；如果描述中还要重复API的名称的话，那就没有提供更多的信息。举个例子：
```
/**
 * Sets the tool tip text.
 *
 * @param text  the text of the tool tip
 */
public void setToolTipText(String text) {
```
上面这段代码对于方法的描述基本上就是把方法名拿出来重写了一遍；这个注解并没有什么卵用。推荐的写法是完整的定义这个工具提示是什么以及返回的文本在什么情况下显示
```
/**
 * Registers the text to display in a tool tip.   The text 
 * displays when the cursor lingers over the component.
 *
 * @param text  the string to display.  If the text is null, 
 *              the tool tip is turned off for this component.
 */
public void setToolTipText(String text) {
```
###当你在使用field这个术语的时候一定要指明清楚
区别静态变量，普通变量。
###避免使用拉丁文

##匿名内部类
Javadoc 工具是不能直接生产匿名内部类的文档的。匿名内部类的声明和文档注释都是被忽略的。如果你想给一个匿名内部类添加注解文档，那么比较好的方法是通过给他外部的类或者调用它的方法上添加注解。
</br>举个例子：
</br>如果你想给makeTree方法中用到的匿名内部类TreeSelectionListener添加一个注解。你可以在makeTree的方法中添加注解。
```
 /**
     * The method used for creating the tree. Any structural 
     * modifications to the display of the Jtree should be done 
     * by overriding this method.
     * <p>
     * This method adds an anonymous TreeSelectionListener to 
     * the returned JTree.  Upon receiving TreeSelectionEvents, 
     * this listener calls refresh with the selected node as a 
     * parameter. 
     */
    public JTree makeTree(AreaInfo ai){
    }
```
###Sample
```
/**
 * Graphics is the abstract base class for all graphics contexts
 * which allow an application to draw onto components realized on
 * various devices or onto off-screen images.
 * A Graphics object encapsulates the state information needed
 * for the various rendering operations that Java supports.  This
 * state information includes:
 * <ul>
 * <li>The Component to draw on
 * <li>A translation origin for rendering and clipping coordinates
 * <li>The current clip
 * <li>The current color
 * <li>The current font
 * <li>The current logical pixel operation function (XOR or Paint)
 * <li>The current XOR alternation color
 *     (see <a href="#setXORMode">setXORMode</a>)
 * </ul>
 * <p>
 * Coordinates are infinitely thin and lie between the pixels of the
 * output device.
 * Operations which draw the outline of a figure operate by traversing
 * along the infinitely thin path with a pixel-sized pen that hangs
 * down and to the right of the anchor point on the path.
 * Operations which fill a figure operate by filling the interior
 * of the infinitely thin path.
 * Operations which render horizontal text render the ascending
 * portion of the characters entirely above the baseline coordinate.
 * <p>
 * Some important points to consider are that drawing a figure that
 * covers a given rectangle will occupy one extra row of pixels on
 * the right and bottom edges compared to filling a figure that is
 * bounded by that same rectangle.
 * Also, drawing a horizontal line along the same y coordinate as
 * the baseline of a line of text will draw the line entirely below
 * the text except for any descenders.
 * Both of these properties are due to the pen hanging down and to
 * the right from the path that it traverses.
 * <p>
 * All coordinates which appear as arguments to the methods of this
 * Graphics object are considered relative to the translation origin
 * of this Graphics object prior to the invocation of the method.
 * All rendering operations modify only pixels which lie within the
 * area bounded by both the current clip of the graphics context
 * and the extents of the Component used to create the Graphics object.
 * 
 * @author      Sami Shaio
 * @author      Arthur van Hoff
 * @version     %I%, %G%
 * @since       1.0
 */
public abstract class Graphics {

    /** 
     * Draws as much of the specified image as is currently available
     * with its northwest corner at the specified coordinate (x, y).
     * This method will return immediately in all cases, even if the
     * entire image has not yet been scaled, dithered and converted
     * for the current output device.
     * <p>
     * If the current output representation is not yet complete then
     * the method will return false and the indicated 
     * {@link ImageObserver} object will be notified as the
     * conversion process progresses.
     *
     * @param img       the image to be drawn
     * @param x         the x-coordinate of the northwest corner
     *                  of the destination rectangle in pixels
     * @param y         the y-coordinate of the northwest corner
     *                  of the destination rectangle in pixels
     * @param observer  the image observer to be notified as more
     *                  of the image is converted.  May be 
     *                  <code>null</code>
     * @return          <code>true</code> if the image is completely 
     *                  loaded and was painted successfully; 
     *                  <code>false</code> otherwise.
     * @see             Image
     * @see             ImageObserver
     * @since           1.0
     */
    public abstract boolean drawImage(Image img, int x, int y, 
                                      ImageObserver observer);


    /**
     * Dispose of the system resources used by this graphics context.
     * The Graphics context cannot be used after being disposed of.
     * While the finalization process of the garbage collector will
     * also dispose of the same system resources, due to the number
     * of Graphics objects that can be created in short time frames
     * it is preferable to manually free the associated resources
     * using this method rather than to rely on a finalization
     * process which may not happen for a long period of time.
     * <p>
     * Graphics objects which are provided as arguments to the paint
     * and update methods of Components are automatically disposed
     * by the system when those methods return.  Programmers should,
     * for efficiency, call the dispose method when finished using
     * a Graphics object only if it was created directly from a
     * Component or another Graphics object.
     *
     * @see       #create(int, int, int, int)
     * @see       #finalize()
     * @see       Component#getGraphics()
     * @see       Component#paint(Graphics)
     * @see       Component#update(Graphics)
     * @since     1.0
     */
    public abstract void dispose();

    /**
     * Disposes of this graphics context once it is no longer 
     * referenced.
     *
     * @see       #dispose()
     * @since     1.0
     */
    public void finalize() {
        dispose();
    }
}
```

#Live Template
路径：
>File -> Settings -> Editor -> Live Templates

第一步：添加模版
</br>![添加模版](https://github.com/mime-mob/JavaDoc_Guide/blob/master/img/pic6.png)
</br>Abbreviation： 表示快捷输入关键字
</br>第二步：在代码编辑页面输入关键字
</br>![使用](https://github.com/mime-mob/JavaDoc_Guide/blob/master/img/pic7.png)
</br>第三步：生成代码块
![生成代码](https://github.com/mime-mob/JavaDoc_Guide/blob/master/img/pic8.png)

