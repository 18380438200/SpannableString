# SpannableString
SpannableString给TextView设置各种样式

SpannableString(标签文本)，可以用来显示复合文本，我们可以通过SpannableString给文本设置各种各样的样式。比如部分文本变色，商城打折的删除线，粗体，斜体，不同大小的文字，文字混合表情，文字点击链接等。TextView通过设置SpannableString后功能就异常强大了，在自定义的Span的情况下，可以说就要上天了。

#####认识SpannableString：
在TextView的public final void setText(CharSequence text)方法中，设置文本，那么这个我们每天都要用的CharSequence到底是什么呢？看Google的官方文档：

![image.png](http://upload-images.jianshu.io/upload_images/8669504-71eb7514e21a98c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

SpannableString继承于CharSequence，所以通过textView.setText(spannableString)的方式使用。SpannableString构造方法参数传入需要设置样式的文本。

######public void setSpan(Object what, int start, int end, int flags)
what为各种类型Span，start为起始位置，end为结束位置，flags为开闭区间的标致。

######flags类型：
- Spanned.SPAN_EXCLUSIVE_EXCLUSIVE 开开区间，如(0,1)
- Spanned.SPAN_INCLUSIVE_EXCLUSIVE 闭开区间，如[0,1)
- Spanned.SPAN_EXCLUSIVE_INCLUSIVE 开闭区间，如(0,1]
- Spanned.SPAN_INCLUSIVE_INCLUSIVE 闭闭区间，如[0,1]

######使用步骤：
1. 创建SpannableString，构造方法设置文本
2. 创建Span,SpannableString.setSpan()
3. textView.setText(spannableString)

- #####ForegroundColorSpan 设置文字前景色（文字颜色）
![image.png](http://upload-images.jianshu.io/upload_images/8669504-287683be7995f338.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getForegroundColorSpan(Context context){
        SpannableString spannableString = new SpannableString("我已同意抖音使用协议");
        ForegroundColorSpan foregroundColorSpan = new ForegroundColorSpan(context.getResources().getColor(R.color.colorPrimary));
        spannableString.setSpan(foregroundColorSpan,4,spannableString.length(), Spanned.SPAN_INCLUSIVE_INCLUSIVE);
        return spannableString;
    }
```

- BackgroundColorSpan 设置文字背景色
![image.png](http://upload-images.jianshu.io/upload_images/8669504-ea1447322c9f9067.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getBackgroundColorSpan(Context context){
        SpannableString spannableString = new SpannableString("你看我头像牛逼不？");
        BackgroundColorSpan backgroundColorSpan = new BackgroundColorSpan(context.getResources().getColor(R.color.colorAccent));
        spannableString.setSpan(backgroundColorSpan,3,5,Spanned.SPAN_INCLUSIVE_INCLUSIVE);
        return spannableString;
    }
```

- StrikethroughSpan 设置删除线
![image.png](http://upload-images.jianshu.io/upload_images/8669504-b0d88303a85744b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getStrikethroughSpan(){
        SpannableString spannableString = new SpannableString("尤龙的传人");
        StrikethroughSpan strikethroughSpan = new StrikethroughSpan();
        spannableString.setSpan(strikethroughSpan,0,1,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        return spannableString;
    }
```

- UnderlineSpan 设置下划线
![image.png](http://upload-images.jianshu.io/upload_images/8669504-7bad5468890e36c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getUnderlineSpan(){
        SpannableString spannableString = new SpannableString("这里是下划线");
        UnderlineSpan underlineSpan = new UnderlineSpan();
        spannableString.setSpan(underlineSpan,3,6,Spanned.SPAN_INCLUSIVE_INCLUSIVE);
        return spannableString;
    }
```

- ScaleXSpan 设置X轴方向拉伸，ScaleXSpan构造方法参数传缩放倍数
![image.png](http://upload-images.jianshu.io/upload_images/8669504-aba1cfc7739d649d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getScaleXSpan(){
        SpannableString spannableString = new SpannableString("媳妇你长胖了");
        ScaleXSpan scaleXSpan = new ScaleXSpan(2);
        spannableString.setSpan(scaleXSpan,0,spannableString.length(),Spanned.SPAN_INCLUSIVE_INCLUSIVE);
        return spannableString;
    }
```

- RelativeSizeSpan 设置文字比例大小，原文字大小基数为1，构造函数参数为float值，缩放为原来比例，给文字依序设置不同大小。
![image.png](http://upload-images.jianshu.io/upload_images/8669504-6d3d6fccf077a531.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getRelativeSizeSpan(){
        SpannableString spannableString = new SpannableString("我心情忐忑不安七上八下");
        RelativeSizeSpan sizeSpan1 = new RelativeSizeSpan(1.2f);
        RelativeSizeSpan sizeSpan2 = new RelativeSizeSpan(1.4f);
        RelativeSizeSpan sizeSpan3 = new RelativeSizeSpan(1.6f);
        RelativeSizeSpan sizeSpan4 = new RelativeSizeSpan(1.8f);

        spannableString.setSpan(sizeSpan1,0,1,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan2,1,2,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan3,2,3,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan4,3,4,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan3,4,5,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan2,5,6,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan1,6,7,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan2,7,8,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan3,8,9,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan4,9,10,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);

        return spannableString;
    }
```

- SuperscriptSpan 设置上标，给平方这个2设置为上标，并且文字缩小。当然这个在望京买套房是我奢侈的梦想。
![image.png](http://upload-images.jianshu.io/upload_images/8669504-e34df94aac37fb26.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getSuperscriptSpan(){
        SpannableString spannableString = new SpannableString("刚在北京望京买了套1202m的房子");
        SuperscriptSpan superscriptSpan = new SuperscriptSpan();
        RelativeSizeSpan sizeSpan = new RelativeSizeSpan(0.7f);
        spannableString.setSpan(superscriptSpan,12,13,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan,12,13,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        return spannableString;
    }
```

- SubscriptSpan设置下标，给这个2设置为下标并缩小。
![image.png](http://upload-images.jianshu.io/upload_images/8669504-ced413080ab3ced2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getSubscriptSpan(){
        SpannableString spannableString = new SpannableString("水分子化学式为H20");
        SubscriptSpan subscriptSpan = new SubscriptSpan();
        RelativeSizeSpan sizeSpan = new RelativeSizeSpan(0.7f);
        spannableString.setSpan(subscriptSpan,8,9,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(sizeSpan,8,9,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        return spannableString;
    }
```

- StyleSpan设置粗体、斜体样式：Typeface.BOLD为粗体字，Typeface.ITALIC为斜体字类型。
![image.png](http://upload-images.jianshu.io/upload_images/8669504-3aaeb9a0703da04e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getStyleSpan(){
        SpannableString spannableString = new SpannableString("身正不怕影子歪");
        StyleSpan styleSpanBold = new StyleSpan(Typeface.BOLD);
        StyleSpan styleSpanitalic = new StyleSpan(Typeface.ITALIC);
        spannableString.setSpan(styleSpanBold,0,4,Spanned.SPAN_INCLUSIVE_INCLUSIVE);
        spannableString.setSpan(styleSpanitalic,4,6,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        return spannableString;
    }
```



- ImageSpan 图文混合，比如在聊天中带有表情图标。这个是文字替换功能，将对应位置的字符替换为图标，这里将文本的空格替换为fx图标；drawable.setBounds()可设置图标的大小。
![image.png](http://upload-images.jianshu.io/upload_images/8669504-c44e48fe9baf9d98.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/800)

```
    public static SpannableString getImageSpan(Context context){
        SpannableString spannableString = new SpannableString("芭芭拉小魔仙 魔法棒");
        Drawable drawable = context.getResources().getDrawable(R.mipmap.fx);
        drawable.setBounds(0,0,70,70);
        ImageSpan imageSpan = new ImageSpan(drawable);
        spannableString.setSpan(imageSpan,6,7,Spanned.SPAN_INCLUSIVE_EXCLUSIVE);
        return spannableString;
    }
```

- ClickableSpan可点击标签，textview需设置：红色带下滑先的“哪里”，就是可点击范围，ClickableSpan自带点击回调。
![giphy (1).gif](http://upload-images.jianshu.io/upload_images/8669504-e6f49afddc88bd6c.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

tvClick.setMovementMethod(LinkMovementMethod.getInstance())方法，textview才会响应点击事件
        //设置点击后文字没有背景
        textView.setHighlightColor(getResources().getColor(android.R.color.transparent));
```
    public static SpannableString getClickableSpan(final Context context){
        SpannableString spannableString = new SpannableString("哪里不会点哪里，so easy！");
        ClickableSpan clickableSpan = new ClickableSpan() {
            @Override
            public void onClick(View widget) {
                Toast.makeText(context,"你戳中我了",Toast.LENGTH_SHORT).show();
            }

            @Override
            public void updateDrawState(TextPaint ds) {
                //设置去掉点击文字下划线
                ds.setUnderlineText(false);
            }
        };
        spannableString.setSpan(clickableSpan,5,7,Spanned.SPAN_INCLUSIVE_INCLUSIVE);
        return spannableString;
    }
```

- URLSpan跳转链接，可以设置为打电话，发短信，发邮件，打开网页等功能；类似于Intent的打电话，发短信，发邮件，打开网页的功能。
![giphy.gif](http://upload-images.jianshu.io/upload_images/8669504-40a82689e1d9c302.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
    public static SpannableString getURLSpan(){
        SpannableString spannableString = new SpannableString("打电话，发短信，发邮件，打开网页");
        spannableString.setSpan(new URLSpan("tel:10086"), 0, 3, Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(new URLSpan("smsto:10086"), 4, 7, Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(new URLSpan("mailto:88888888@qq.com"), 8, 11, Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
        spannableString.setSpan(new URLSpan("http://www.jianshu.com"), 12, 16, Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
        return spannableString;
    }
```
