# RelativeLayout #
> Use RelativeLayout to create UIs that scale to fit any screen size.

>使用相对布局，创建可以适应任何屏幕大小，自动缩放的用户界面。

RelativeLayout is used to position and size views relative to properties of the layout or sibling views. Unlike AbsoluteLayout, RelativeLayout does not have the concept of the moving anchor and does not have facilities for positioning elements relative to the bottom or right edges of the layout. RelativeLayout does support positioning elements outside of its own bounds.

RelativeLayout用于定位视图和设置其尺寸大小，相对于布局或兄弟姐妹视图的属性。与AbsoluteLayout不同，RelativeLayout没有移动锚的概念,没有设施定位元素相对于底部或右边缘的布局。RelativeLayout支持定位自己的界限以外的元素。

![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/relative-layout/Images/Layouts-sml.png)

## Purpose ##
>RelativeLayout can be used to position views on screen relative to the overall layout or two other views.

>RelativeLayout可用于定位相对于屏幕上的视图，或相对于其它视图。

![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/relative-layout/Images/flag.png)

## Usage ##
### Understanding Constraints ###
### 理解约束 ###
Positioning and sizing a view within a RelativeLayout is done with constraints. A constraint expression can include the following information:
在相对布局中，定位视图和设置视图大小是通过约束来完成的。一个约束表达式可以包含以下信息:

- Type – whether the constraint is relative to the parent or to another view.
- Type 约束是相对于父元素，或是另一个视图。 RelativeToParent/RelativeToView
- Property – which property to use as the basis for the constraint.
- Property 哪个属性作为约束的基础。
- Factor – the factor to apply to the property value.
- 因素——适用于属性值的因素。
- Constant – the value to use as an offset of the value.
- 常量 - 常量值作为一个偏移量的值。
- ElementName – the name of the view that the constraint is relative to.
- ElementName - 约束相对视图的名称。

In XAML, constraints are expressed as ConstraintExpressions. Consider the following example:
```xml
<BoxView Color="Green" WidthRequest="50" HeightRequest="50"
    RelativeLayout.XConstraint =
      "{ConstraintExpression Type=RelativeToParent,
                             Property=Width,
                             Factor=0.5,
                             Constant=-100}"
    RelativeLayout.YConstraint =
      "{ConstraintExpression Type=RelativeToParent,
                             Property=Height,
                             Factor=0.5,
                             Constant=-100}" />
```

In C#, constraints are expressed a little differently, using functions rather than expressions on the view. Constraints are specified as arguments to the layout's Add method:
```c#
layout.Children.Add(box, Constraint.RelativeToParent((parent) =>
    {
      return (.5 * parent.Width) - 100;
    }),
    Constraint.RelativeToParent((parent) =>
    {
        return (.5 * parent.Height) - 100;
    }),
    Constraint.Constant(50), Constraint.Constant(50));
```

Note the following aspects of the above layout:
上面的布局需要注意以下几个方面:

- The x and y constraints are specified with their own constraints.
- x和y约束明确指定他们自己的约束。
- In C#, relative constraints are defined as functions. Concepts like Factor aren't there, but can be implemented manually.
- 在c#中,相对约束是定义为方法。没有因素概念,但是可以手动地实现。
- The box's x coordinate is defined as half the width of the parent, -100.
- box的x坐标定义为父元素宽度的一半,再减去100。
- The box's y coordinate is defined as half the height of the parent, -100.
- box的y坐标定义为父元素高度的一半，再减去100。


Note: Because of the way constraints are defined, it is possible to make more complex layouts in C# than can be specified with XAML.
注意:由于约束定义的方法,在C#中比在XAML中可以创造更复杂的布局。

Both of the examples above define constraints as RelativeToParent – that is, their values are relative to the parent element. It is also possible to define constraints as relative to another view. This allows for more intuitive (to the developer) layouts and can make the intent of your layout code more readily apparent.

上面两个示例约束定义为RelativeToParent——也就是说,它们的值都是相对于父元素。还可以约束定义为相对于另一个视图。这允许更直观(开发人员)布局和可以使布局代码的意图更显而易见。

Consider a layout where one element needs to be 20 pixels lower than another. If both elements are defined with constant values, the lower could have its Y constraint defined as a constant that is 20 pixels greater than the Y constraint of the higher element. That approach falls short if the higher element is positioned using a proportion, so that the pixel size isn't known. In that case, constraining the element based on another element's position is more robust:

考虑这样一个布局,一个元素比另一个低20个像素。如果两个元素定义常量值,降低其Y约束定义为一个常数,是20像素大于Y更高的元素的约束。这种方法不足,如果元素是定位使用比例越高,像素大小不得而知。在这种情况下,约束元素基于另一个元素的位置是更健壮可靠的:

```xml
<RelativeLayout>
    <BoxView Color="Red" x:Name="redBox"
        RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent,
            Property=Height,Factor=.15,Constant=0}"
        RelativeLayout.WidthConstraint="{ConstraintExpression
            Type=RelativeToParent,Property=Width,Factor=1,Constant=0}"
        RelativeLayout.HeightConstraint="{ConstraintExpression
            Type=RelativeToParent,Property=Height,Factor=.8,Constant=0}" />
    <BoxView Color="Blue"
        RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToView,
            ElementName=redBox,Property=Y,Factor=1,Constant=20}"
        RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToView,
            ElementName=redBox,Property=X,Factor=1,Constant=20}"
        RelativeLayout.WidthConstraint="{ConstraintExpression
            Type=RelativeToParent,Property=Width,Factor=.5,Constant=0}"
        RelativeLayout.HeightConstraint="{ConstraintExpression
            Type=RelativeToParent,Property=Height,Factor=.5,Constant=0}" />
</RelativeLayout>
```
To accomplish the same layout in C#:
用c#实现相同的布局:
```c#
layout.Children.Add (redBox, Constraint.RelativeToParent ((parent) => {
        return parent.X;
    }), Constraint.RelativeToParent ((parent) => {
        return parent.Y * .15;
    }), Constraint.RelativeToParent((parent) => {
        return parent.Width;
    }), Constraint.RelativeToParent((parent) => {
        return parent.Height * .8;
    }));
layout.Children.Add (blueBox, Constraint.RelativeToView (redBox, (Parent, sibling) => {
        return sibling.X + 20;
    }), Constraint.RelativeToView (blueBox, (parent, sibling) => {
        return sibling.Y + 20;
    }), Constraint.RelativeToParent((parent) => {
        return parent.Width * .5;
    }), Constraint.RelativeToParent((parent) => {
        return parent.Height * .5;
    }));
```

This produces the following output, with the blue box's position determined relative to the position of the red box:

这产生以下输出,蓝框的位置确定相对于红盒子的位置:

![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/relative-layout/Images/red_blue_box.png)

## Sizing ##
Views laid out by RelativeLayout have two options for specifying their size:
在相对布局中，视图的显示有两个选项用于指定它们的大小:

- HeightRequest & WidthRequest
- RelativeLayout.WidthConstraint & RelativeLayout.HeightConstraint

HeightRequest and WidthRequest specify the intended height and width of the view, but may be overridden by layouts as needed. WidthConstraint and HeightConstraint support setting the height and width as a value relative to the layout's or another view's properties, or as a constant value.

HeightRequest和WidthRequest指定视图的高度和宽度,但可以根据需要被布局覆盖。WidthConstraint和HeightConstraint支持设置高度和宽度值相对于布局或另一个视图的属性,或是一个常数值。

## Exploring a Complex Layout ##
## 探索一个复杂的布局 ##

Each of the layouts have strengths and weaknesses for creating particular layouts. Throughout this series of layout articles, a sample app has been created with the same page layout implemented using three different layouts.

每个布局都有优缺点。在本系列布局文章中,创建了一个示例应用程序相同的页面布局使用三种不同的布局实现的。

Consider the following XAML:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
x:Class="TheBusinessTumble.RelativeLayoutPage"
BackgroundColor="Maroon"
Title="RelativeLayout">
    <ContentPage.Content>
    <ScrollView>
      <RelativeLayout>
        <BoxView Color="Gray" HeightRequest="100"
            RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=1}" />
        <Button BorderRadius="35" x:Name="imageCircleBack"
            BackgroundColor="Maroon" HeightRequest="70" WidthRequest="70" RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent,Property=Width, Factor=.5, Constant = -35}" RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Factor=0, Property=Y, Constant=70}" />
        <Button BorderRadius="30" BackgroundColor="Red" HeightRequest="60"
            WidthRequest="60" RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToView, ElementName=imageCircleBack, Property=X, Factor=1,Constant=5}" RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Factor=0, Property=Y, Constant=75}" />
        <Label Text="User Name" FontAttributes="Bold" FontSize="26"
            HorizontalTextAlignment="Center" RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Y, Factor=0, Constant=140}" RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=1}" />
        <Entry Text="Bio + Hashtags" TextColor="White" BackgroundColor="Maroon"
            RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Y, Factor=0, Constant=180}" RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=1}" />
        <RelativeLayout BackgroundColor="White" RelativeLayout.YConstraint="
            {ConstraintExpression Type=RelativeToParent, Property=Y, Factor=0, Constant=220}" HeightRequest="60" RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=1}" >
            <BoxView BackgroundColor="Black" WidthRequest="50"
                HeightRequest="50" RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Y, Factor=0, Constant=5}" RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=X, Factor=0, Constant=5}" />
            <BoxView BackgroundColor="Maroon" WidthRequest="50"
                HeightRequest="50" RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Y, Factor=0, Constant=5}" RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0.5, Constant=}" />
            <Label FontSize="14" TextColor="Black" Text="Accent Color"
                RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Y, Factor=0, Constant=20}" RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=X, Factor=0, Constant=60}" />
            <Label FontSize="14" TextColor="Black" Text="Primary Color"
                RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Y, Factor=0, Constant=20}" RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0.5, Constant=55}" />
        </RelativeLayout>
        <RelativeLayout Padding="5,0,0,0">
          <Label FontSize="14" Text="Age:" TextColor="White"
            RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=305}"
            RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0, Constant=10}"
            RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width,Factor=.25,Constant=0}"
            RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=50}" />
          <Entry Text="35" TextColor="White" BackgroundColor="Maroon"
            RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=280}"
            RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0.3, Constant=0}"
            RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width,Factor=0.75,Constant=0}"
            RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=50}" />
        </RelativeLayout>
        <RelativeLayout  Padding="5,0,0,0">
          <Label FontSize="14" Text="Interests:" TextColor="White"
            RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=345}"
            RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0, Constant=10}"
            RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width,Factor=.25,Constant=0}"
            RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=50}" />
          <Entry Text="Xamarin.Forms" TextColor="White" BackgroundColor="Maroon"
            RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=320}"
            RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0.3, Constant=0}"
            RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width,Factor=0.75,Constant=0}"
            RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=50}" />
        </RelativeLayout>
        <RelativeLayout  Padding="5,0,0,0">
          <Label FontSize="14" Text="Ask me about:" TextColor="White"
            LineBreakMode="WordWrap"
            RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=395}"
            RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0, Constant=10}"
            RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width,Factor=.25,Constant=0}"
            RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=50}" />
          <Entry Text="Xamarin, C#, .NET, Mono" TextColor="White"
            BackgroundColor="Maroon"
            RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=370}"
            RelativeLayout.XConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width, Factor=0.3, Constant=0}"
            RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent, Property=Width,Factor=0.75,Constant=0}"
            RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=0,Constant=50}" />
        </RelativeLayout>
      </RelativeLayout>
    </ScrollView>
  </ContentPage.Content>
</ContentPage>
```

The above code results in the following layout:
https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/relative-layout/Images/relative.png

Note that, due to a difference in how buttons are rendered by Windows Phone, some of the circles have been replaced by boxviews in the Windows Phone screenshot.

Notice that RelativeLayoutss are nested, because in some cases nesting layouts can be easier than presenting all elements within the same layout. Also notice that some elements are RelativeToView, because that allows for easier and more intuitive layout when the relationships between views guide positioning.

注意RelativeLayoutss是嵌套的,因为在某些情况下可以简单地嵌套布局呈现所有元素在相同的布局。也注意到一些元素RelativeToView,因为可以更容易和更直观的布局当观点指导定位之间的关系。
