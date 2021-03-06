# AbsoluteLayout #
[原文链接](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/absolute-layout/)

>Use AbsoluteLayout to create pixel-perfect UIs.

>使用绝对布局来创建完美像素级用户界面。


AbsoluteLayout positions and sizes child elements proportional to its own size and position or by absolute values. Child views may be positioned and sized using proportional values or static values, and proportional and static values can be mixed.

![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/absolute-layout/Images/Layouts.png)

This article will cover:

- Purpose – common uses for AbsoluteLayout.
- Usage – how to use AbsoluteLayout to achieve your desired design.
    - Proportional Layouts – understand how proportional values work in an AbsoluteLayout.
    - 按比例布局
    - Specifying Values – understand how proportional and absolute values are specified.
    - 具体值
    - Proportional Values – understand how proportional values work.
    - 比例值
    - Absolute Values – understand how absolute values work.
    - 绝对值

## Purpose ##
Because of the positioning model of AbsoluteLayout, the layout makes it relatively straightforward to position elements so that they are flush with any side of the layout, or centered. With proportional sizes and positions, elements in an AbsoluteLayout can scale automatically to any view size. For items where only the position but not the size should scale, absolute and proportional values can be mixed.

由于绝对布局的定位模型,布局使其相对简单的元素位置,这样他们填充到边缘，或是居中。使用相对比例的尺寸和坐标,元素在绝对布局中可以自动扩展到任意大小。只有坐标位置而不是尺寸大小应该被缩放，绝对和相对比例值可以混合使用。

AbsoluteLayout could be used anywhere elements need to be positioned within a view and is especially useful when aligning elements to edges.

绝对布局可以使用任何元素需要被定位在一个视图和调整元素的边缘时尤其有用。

## Usage ##
### Proportional Layouts ###
AbsoluteLayout has a unique anchor model whereby the anchor of the element is positioned relative to its element as the element is positioned relative to the layout when proportional positioning is used. When absolute positioning is used, the anchor is at (0,0) within the view. This has two important consequences:

绝对布局有独特的锚模型即锚元素的位置相对于它的元素的元素的位置相对于布局比例定位时使用。当使用绝对定位时,锚在(0,0)在视图。这有两个重要的后果:

- Elements cannot be positioned off screen using proportional values.
- 元素不能使用比例值定位到屏幕外。
- Elements can be reliably positioned along any side of the layout or in the center, regardless of the size of the layout or device.
- 元素可以可靠地定位在任何一边的布局或中心,无论大小的布局或设备。

AbsoluteLayout, like RelativeLayout, is able to position elements so that they overlap.

绝对布局像相对布局一样,能够定位元素重叠。

Note in the following screenshot, the anchor of the box is a white dot. Notice the relationship between the anchor and the box as it moves through the layout:

注意在以下截图,盒子的锚是一个白色的点。注意锚和盒子之间的关系在整个布局:

![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/absolute-layout/Images/anchor_start.png)

![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/absolute-layout/Images/anchor_center.png)

![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/absolute-layout/Images/anchor_end.png)

## Specifying Values ##
Views within an AbsoluteLayout are positioned using four values:

绝对布局中的视图使用四个值来进行定位:

- X – the x (horizontal) position of the view's anchor
- X坐标
- Y – the y (vertical) position of the view's anchor
- Y坐标
- Width – the width of the view
- 宽度
- Height – the height of the view
- 高度

Each of those values can be set as a proportional value or an absolute value.

这些值可以设置为一个比例值或一个绝对的价值。

Values are specified as a combination of bounds and a flag. LayoutBounds is a Rectangle consisting of four values: x, y, width, height.

值被指定为边界和标志的组合。LayoutBounds组成的一个矩形四个值:x轴坐标,y轴坐标,宽度、高度。

## AbsoluteLayoutFlags ##
AbsoluteLayoutFlags specifies how values will be interpreted and has the following predefined options:

AbsoluteLayoutFlags指定值将如何解释，具有以下预定义的选项:

- None – interprets all values as absolute. This is the default value if no layout flags are specified.
- 默认值，把所有值用于绝对布局。
- All – interprets all values as proportional.
- 解释所有值成比例。
- WidthProportional – interprets the Width value as proportional and all other values as absolute.
- 宽度值为按比例，其它值为绝对。
- HeightProportional – interprets only the height value as proportional with all other values absolute.
- 高度值为按比例，其它值为绝对。
- XProportional – interprets the X value as proportional, while treating all other values as absolute.
- X坐标是按比例，其它值为绝对。
- YProportional – interprets the Y value as proportional, while treating all other values as absolute.
- Y坐标是按比例，其它值为绝对。
- PositionProportional – interprets the X and Y values as proportional, while the size values are interpreted as absolute.
- X和Y坐标是按比例，其它是绝对。
- SizeProportional – interprets the Width and Height values as proportional while the position values are absolute.
- 宽度和高度是按比例，……

In XAML, bounds and flags are set as part of the definition of views within the layout, using the AbsoluteLayout.LayoutBounds property. Bounds are set as a comma-separated list of values, X, Y, Width, and Height, in that order. Flags are also specified in the declaration of views in the layout using the AbsoluteLayout.LayoutFlags property. Note that flags can be combined in XAML using a comma-separated list. Consider the following example:

在XAML,界限和标志作为设置，是属于布局视图定义的一部分,使用AbsoluteLayout.LayoutBounds属性。边界设置为一个以逗号分隔的值，以X,Y,宽度,高度这样的顺序。Flags也在声明中指定使用AbsoluteLayout.LayoutFlags属性。注意Flags标志可以组合在XAML使用逗号分隔的列表。考虑下面的例子:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
x:Class="LayoutSamples.AbsoluteLayoutExploration"
Title="Absolute Layout Exploration">
    <ContentPage.Content>
        <AbsoluteLayout>
            <Label Text="I'm centered on iPhone 4 but no other device"
                AbsoluteLayout.LayoutBounds="115,150,100,100" LineBreakMode="WordWrap"  />
            <Label Text="I'm bottom center on every device."
                AbsoluteLayout.LayoutBounds=".5,1,.5,.1" AbsoluteLayout.LayoutFlags="All"
                LineBreakMode="WordWrap"  />
            <BoxView Color="Olive"  AbsoluteLayout.LayoutBounds="1,.5, 25, 100"
                AbsoluteLayout.LayoutFlags="PositionProportional" />
            <BoxView Color="Red" AbsoluteLayout.LayoutBounds="0,.5,25,100"
                AbsoluteLayout.LayoutFlags="PositionProportional" />
            <BoxView Color="Blue" AbsoluteLayout.LayoutBounds=".5,0,100,25"
                AbsoluteLayout.LayoutFlags="PositionProportional" />
        </AbsoluteLayout>
    </ContentPage.Content>
</ContentPage>
```

![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/absolute-layout/Images/exploration.png)

Note the following:

注意:

- The label in the center is positioned using absolute size and position values. Because of that, it appears centered on iPhone 4S and lower, but not centered on larger devices.
- 中心Label标签是使用绝对的尺寸和位置值进行定位的。因为这样,在iPhone 4s以及低版本中它似乎集中在中间，但在更大的设备上就不在中间了。
- The text at the bottom of the layout is positioned using proportional size and position values. It will always appear at the bottom center of the layout, but its size will grow with larger layout sizes.
- 底部的文本的布局定位使用比例大小和位置值。它总是出现在底部中心的布局,但布局尺寸将会随着大布局尺寸而增长。
- Three colored BoxViews are positioned at the top, left, and right edges of the screen using proportional position and absolute size.
- 三个彩色BoxViews定位在屏幕的顶部,左,和右，使用比例位置和绝对大小。

The following achieves the same layout in C#:

以下达到相同的布局在c#中:
```c#
public class AbsoluteLayoutExplorationCode : ContentPage
{
    public AbsoluteLayoutExplorationCode ()
    {
        Title = "Absolute Layout Exploration - Code";
        var layout = new AbsoluteLayout();

        var centerLabel = new Label {
        Text = "I'm centered on iPhone 4 but no other device.",
        LineBreakMode = LineBreakMode.WordWrap};

        AbsoluteLayout.SetLayoutBounds (centerLabel, new Rectangle (115, 159, 100, 100));
        // No need to set layout flags, absolute positioning is the default

        var bottomLabel = new Label { Text = "I'm bottom center on every device.", LineBreakMode = LineBreakMode.WordWrap };
        AbsoluteLayout.SetLayoutBounds (bottomLabel, new Rectangle (.5, 1, .5, .1));
        AbsoluteLayout.SetLayoutFlags (bottomLabel, AbsoluteLayoutFlags.All);

        var rightBox = new BoxView{ Color = Color.Olive };
        AbsoluteLayout.SetLayoutBounds (rightBox, new Rectangle (1, .5, 25, 100));
        AbsoluteLayout.SetLayoutFlags (rightBox, AbsoluteLayoutFlags.PositionProportional);

        var leftBox = new BoxView{ Color = Color.Red };
        AbsoluteLayout.SetLayoutBounds (leftBox, new Rectangle (0, .5, 25, 100));
        AbsoluteLayout.SetLayoutFlags (leftBox, AbsoluteLayoutFlags.PositionProportional);

        var topBox = new BoxView{ Color = Color.Blue };
        AbsoluteLayout.SetLayoutBounds (topBox, new Rectangle (.5, 0, 100, 25));
        AbsoluteLayout.SetLayoutFlags (topBox, AbsoluteLayoutFlags.PositionProportional);

        layout.Children.Add (bottomLabel);
        layout.Children.Add (centerLabel);
        layout.Children.Add (rightBox);
        layout.Children.Add (leftBox);
        layout.Children.Add (topBox);

        Content = layout;
    }
}
```

## Proportional Values ##
## 比例值 ##
Proportional values define a relationship between a layout and a view. This relationship defines a child view's position or scale value as a proportion of the corresponding value of the parent layout. These values are expressed as doubles with values between 0 and 1.

比例值定义一个布局和视图之间的关系。这种关系定义了子视图的位置或缩放值作为父布局的对应值的比例分配。这些值表示为双精度的值在0和1之间。

Proportional values are used to position and size views within the layout. So, when a view's width is set as a proportion, the resultant width value is the proportion multiplied by the AbsoluteLayout's width. For example, with an AbsoluteLayout of width 500 and a view set to have a proportional width of .5, the rendered width of the view will be 250 (500 x .5).

比例值用于布局中视图的位置和大小。所以,当一个视图的宽度设置为比例,合成宽度值比例乘以AbsoluteLayout的宽度。例如,500年的AbsoluteLayout宽度和视图设置为有一个宽度成比例.5、视图的显示宽度是250(500x.5)。

To use proportional values, set LayoutBounds using (x, y) proportions and proportional sizes, then set LayoutFlags to All.

使用比例值,设置LayoutBounds使用(x,y)比例和比例大小,然后设置LayoutFlags为All。

In XAML:
```xml
<Label Text="I'm bottom center on every device."
  AbsoluteLayout.LayoutBounds=".5,1,.5,.1" AbsoluteLayout.LayoutFlags="All"  />
```

In C#:
```c#
var label = new Label {Text = "I'm bottom center on every device."};
AbsoluteLayout.SetLayoutBounds(label, new Rectangle(.5,1,.5,.1));
AbsoluteLayout.SetLayoutFlags(label, AbsoluteLayoutFlags.All);
```

## Absolute Values ##
## 绝对值 ##
Absolute values explicitly define where views should be positioned within the layout. Unlike proportional values, absolute values are capable of positioning and sizing a view that does not fit within the bounds of the layout.

绝对值明确定义视图在布局应该如何定位。不像比例值,绝对值的定位和大小不会去动态适应布局的边界。

Using absolute values for positioning can be dangerous when the size of the layout is not known. When using absolute positions, an element in the center of the screen at one size could be offset at any other size. It is important to test your app across the various screen sizes of your supported devices.

当布局的尺寸大小不清楚的时候，使用绝对值定位可能是危险的。当使用绝对位置时，一个在屏幕的中心的元素的尺寸可能出现尺寸偏移。在您支持的各种屏幕尺寸的设备上测试您的应用程序是很重要的。

To use absolute layout values, set LayoutBounds using (x, y) coordinates and explicit sizes, then set LayoutFlags to None.

使用绝对布局值,设置LayoutBounds使用(x,y)坐标和明确的尺寸,然后设置LayoutFlags值为None。

In XAML:
```xml
<Label Text="I'm centered on iPhone 4 but no other device."
  AbsoluteLayout.LayoutBounds="115,150,100,100"  />
  ```
In C#:
```c#
var label = new Label {Text = "I'm centered on iPhone 4 but no other device."};
AbsoluteLayout.SetLayoutBounds(label, new Rectangle(115,150,100,100));
```

## Exploring a Complex Layout ##
## 探索一个复杂的布局 ##
Each of the layouts have strengths and weaknesses for creating particular layouts. Throughout this series of layout articles, a sample app has been created with the same page layout implemented using three different layouts.

每个布局都有优缺点，在创建特定的布局时。在本系列的布局文章中,创建了一个示例应用程序相同的页面布局使用三种不同的布局实现的。

Consider the following XAML:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
x:Class="TheBusinessTumble.AbsoluteLayoutPage"
Title="AbsoluteLayout">
    <ContentPage.ToolbarItems>
        <ToolbarItem Text="Save" />
    </ContentPage.ToolbarItems>
    <ContentPage.Content>
        <ScrollView>
            <AbsoluteLayout BackgroundColor="Maroon">
                <BoxView BackgroundColor="Gray" AbsoluteLayout.LayoutBounds="0
                    0,1,100" AbsoluteLayout.LayoutFlags="XProportional,YProportional,WidthProportional" />
                <Button BackgroundColor="Maroon"
                    AbsoluteLayout.LayoutBounds=".5,55,70,70" AbsoluteLayout.LayoutFlags="XProportional" BorderRadius="35" />
                <Button BackgroundColor="Red" AbsoluteLayout.LayoutBounds=".5
                    60,60,60" AbsoluteLayout.LayoutFlags="XProportional" BorderRadius="30" />
                <Label Text="User Name" FontAttributes="Bold" FontSize="26"
                    TextColor="Black" HorizontalTextAlignment="Center" AbsoluteLayout.LayoutBounds=".5,140,1,40" AbsoluteLayout.LayoutFlags="XProportional,WidthProportional" />
                <Entry Text="Bio + Hashtags" TextColor="White"
                    BackgroundColor="Maroon" AbsoluteLayout.LayoutBounds=".5,180,1,40" AbsoluteLayout.LayoutFlags="XProportional,WidthProportional" />
                <AbsoluteLayout BackgroundColor="White"
                        AbsoluteLayout.LayoutBounds="0, 220, 1, 50" AbsoluteLayout.LayoutFlags="XProportional,WidthProportional">
                    <AbsoluteLayout AbsoluteLayout.LayoutBounds="0,0,.5,1" AbsoluteLayout.LayoutFlags="WidthProportional,HeightProportional">
                        <Button BackgroundColor="Black" BorderRadius="20"
                            AbsoluteLayout.LayoutBounds="5,.5,40,40" AbsoluteLayout.LayoutFlags="YProportional" />
                        <Label Text="Accent Color" TextColor="Black"
                            AbsoluteLayout.LayoutBounds="50,.55,1,25" AbsoluteLayout.LayoutFlags="YProportional,WidthProportional" />
                    </AbsoluteLayout>
                    <AbsoluteLayout AbsoluteLayout.LayoutBounds="1,0,.5,1" AbsoluteLayout.LayoutFlags="WidthProportional,HeightProportional,XProportional">
                        <Button BackgroundColor="Maroon" BorderRadius="20"
                            AbsoluteLayout.LayoutBounds="5,.5,40,40" AbsoluteLayout.LayoutFlags="YProportional" />
                        <Label Text="Primary Color" TextColor="Black"
                            AbsoluteLayout.LayoutBounds="50,.55,1,25" AbsoluteLayout.LayoutFlags="YProportional,WidthProportional" />
                    </AbsoluteLayout>
                </AbsoluteLayout>
                <AbsoluteLayout AbsoluteLayout.LayoutBounds="0,270,1,50" AbsoluteLayout.LayoutFlags="WidthProportional" Padding="5,0,0,0">
                    <Label Text="Age:" TextColor="White"
                        AbsoluteLayout.LayoutBounds="0,25,.25,50" AbsoluteLayout.LayoutFlags="WidthProportional" />
                    <Entry Text="35" TextColor="White" BackgroundColor="Maroon"
                        AbsoluteLayout.LayoutBounds="1,10,.75,50" AbsoluteLayout.LayoutFlags="XProportional,WidthProportional" />
                </AbsoluteLayout>
                <AbsoluteLayout AbsoluteLayout.LayoutBounds="0,320,1,50" AbsoluteLayout.LayoutFlags="WidthProportional" Padding="5,0,0,0">
                    <Label Text="Interests:" TextColor="White"
                        AbsoluteLayout.LayoutBounds="0,25,.25,50" AbsoluteLayout.LayoutFlags="WidthProportional" />
                    <Entry Text="Xamarin.Forms" TextColor="White"
                        BackgroundColor="Maroon" AbsoluteLayout.LayoutBounds="1,10,.75,50" AbsoluteLayout.LayoutFlags="XProportional,WidthProportional" />
                </AbsoluteLayout>
                <AbsoluteLayout AbsoluteLayout.LayoutBounds="0,370,1,50" AbsoluteLayout.LayoutFlags="WidthProportional" Padding="5,0,0,0">
                    <Label Text="Ask me about:" TextColor="White"
                        AbsoluteLayout.LayoutBounds="0,25,.25,50" AbsoluteLayout.LayoutFlags="WidthProportional" />
                    <Entry Text="Xamarin, C#, .NET, Mono" TextColor="White"
                        BackgroundColor="Maroon" AbsoluteLayout.LayoutBounds="1,10,.75,50" AbsoluteLayout.LayoutFlags="XProportional,WidthProportional" />
                </AbsoluteLayout>
            </AbsoluteLayout>
        </ScrollView>
    </ContentPage.Content>
</ContentPage>
```

The above code results in the following layout:
![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/absolute-layout/Images/abs.png)

Note that, due to a difference in how buttons are rendered by Windows Phone, some of the circles have been replaced by boxviews in the Windows Phone screenshot.

Notice that AbsoluteLayouts are nested, because in some cases nesting layouts can be easier than presenting all elements within the same layout.

注意AbsoluteLayouts是嵌套的,因为在某些情况下可以简单地嵌套布局呈现所有元素在相同的布局。

