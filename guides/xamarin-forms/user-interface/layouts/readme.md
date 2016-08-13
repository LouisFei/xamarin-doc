# Layouts #
[原文链接](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/)

>Lay out views on screen.

Xamarin.Forms has several layouts and features for organizing content on screen. Each layout control is described below, as well as details on how to handle screen orientation changes:

- StackLayout – used to arrange views linearly, either horizontally or vertically. Views in a StackLayout can be aligned to the center, left or right of the layout.
- AbsoluteLayout – used to arrange views by setting coordinates & size in terms of absolute values or ratios. AbsoluteLayout can be used to layer views as well as anchor them to the left, right or center.
- 绝对布局 - 用于排列一组视图，通过设置它们的坐标和尺寸，使用绝对值或比例。绝对布局能被用于放置相对于锚点的左，右，中间对齐。
- RelativeLayout – used to arrange views by setting constraints relative to their parent's dimensions & position.
- Grid – used to arrange views in a grid. Rows and columns can be specified in terms of absolute values or ratios.
- ScrollView – used to provide scrolling when a view can't fit entirely within the bounds of the screen.
- LayoutOptions – define alignment and expansion for a view, relative to its parent.
- Margin and Padding – demonstrates how to control layout behavior when an element is rendered in the user interface.
- Device Orientation – explains how to handle device orientation changes.
- Layout on tablet and desktop devices – shows how to optimize for larger screens on each platform.

Platform controls can also be used directly in Xamarin.Forms layouts with Native Embedding (new in Xamarin.Forms 2.2), and you can create custom layouts to meet specific requirements.

The following graphic visualizes the layout controls:
![](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/Images/Layouts.png)

## Choosing the Right Layout ##
The layouts you choose in your app can either help or hurt you as you're creating an attractive and usable Xamarin.Forms app. Taking some time to consider how each layout works can help you write cleaner and more scalable UI code. A screen can have a combination of different layouts to achieve a specific design.

### StackLayout ###
The StackLayout is used for displaying views along a line that is either horizontal or vertical. Position and size within the layout is determined based on a view's HeightRequest, WidthRequest, HorizontalOptions and VerticalOptions. StackLayout is often used as the base layout, arranging other layouts on the screen.

For an example of when StackLayout would be a good choice, consider an app that needs to display a button and a label, with the label left-aligned and the button right-aligned.

```xml
<StackLayout Orientation="Horizontal">
  <Label HorizontalOptions="StartAndExpand" Text="Label" />
  <Button HorizontalOptions="End" Text="Button" />
</StackLayout>
```

### AbsoluteLayout ###
The AbsoluteLayout is used for displaying views, with size and position being specified either as explicit values or values relative to the size of the layout. Unlike StackLayout and Grid, AbsoluteLayout allows child views to overlap. Unlike RelativeLayout, AbsoluteLayout doesn't let you place elements off screen.

For an example of when AbsoluteLayout would be a good choice, consider an app that needs to present collections of objects as stacks. This is often seen when presenting albums of photos or songs. The following code gives the appearance of a pile, with elements rotated to hint at the contents of the pile:

In XAML:
```xml
<AbsoluteLayout Padding="15">
  <Image AbsoluteLayout.LayoutFlags="PositionProportional" AbsoluteLayout.LayoutBounds="0.5, 0, 100, 100" Rotation="30"
    Source="bottom.png" />
  <Image AbsoluteLayout.LayoutFlags="PositionProportional" AbsoluteLayout.LayoutBounds="0.5, 0, 100, 100" Rotation="60"
    Source="middle.png" />
  <Image AbsoluteLayout.LayoutFlags="PositionProportional" AbsoluteLayout.LayoutBounds="0.5, 0, 100, 100"
    Source="cover.png" />
</AbsoluteLayout>
```

Note the following aspects of the above code:

- Each Image is displayed in the same position (in the middle of the horizontal space)
- The Padding is considered by AbsoluteLayout, unlike RelativeLayout, which ignores it.
- AbsoluteLayout.LayoutFlags specifies how the layout bounds will be interpreted. In this case PositionProportional, means that the coordinates will be a ratio of the size of the layout, while the size will be interpreted as an explicit size.
- AbsoluteLayout.Layoutbounds specifies the horizontal position, vertical position, width and height in that order.

### RelativeLayout ###
The RelativeLayout is used for displaying views, with size and position specified as values relative to the values of the layout or another view. Relative values do not need to match he corresponding value on the related view. As an example, it is possible to set a view's Width property to be proportional to another view's X property.

RelativeLayout can be used to create UIs that scale proportionally across device sizes. The following XAML implements a design with boxes at the topmost corners, with a flagpole with flag in the center:

```xml
<RelativeLayout HorizontalOptions="FillAndExpand" VerticalOptions="FillAndExpand">
  <BoxView Color="Blue" HeightRequest="50" WidthRequest="50"
    RelativeLayout.XConstraint= "{ConstraintExpression Type=RelativeToParent, Property=Width, Factor = 0}"
    RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor = 0}" />
  <BoxView Color="Red" HeightRequest="50" WidthRequest="50"
    RelativeLayout.XConstraint= "{ConstraintExpression Type=RelativeToParent, Property=Width, Factor = .9}"
    RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor = 0}" />
  <BoxView Color="Gray" WidthRequest="15" x:Name="pole"
    RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=.75}"
    RelativeLayout.XConstraint= "{ConstraintExpression Type=RelativeToParent, Property=Width, Factor = .45}"
    RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor = .25}" />
  <BoxView Color="Green"
    RelativeLayout.HeightConstraint="{ConstraintExpression Type=RelativeToParent, Property=Height, Factor=.10, Constant=10}"
    RelativeLayout.WidthConstraint="{ConstraintExpression Type=RelativeToParent,Property=Width, Factor=.2, Constant=20}"
    RelativeLayout.XConstraint= "{ConstraintExpression Type=RelativeToView, ElementName=pole, Property=X, Constant=15}"
    RelativeLayout.YConstraint="{ConstraintExpression Type=RelativeToView, ElementName=pole, Property=Y, Constant=0}" />
</RelativeLayout>
```

Note the following aspects of the above code:

- Both positions and sizes are specified as constraints.
- The flagpole is named so that the flag's (green box's) position can be set relative to the flagpole.
- The constraint expressions have Factor and Constant properties, which can be used to define positions and sizes as multiples (or fractions) of properties of other objects, plus a constant. Constants can be negative.

### Grid ###
The Grid is used for displaying elements in rows & columns. Note that the Grid is not a table, so it does not have the concept of cells, header & footer rows, or borders between rows & columns. In general, Grid is not appropriate for displaying tabular data. For that use, consider a ListView or TableView.

For an example of when a Grid is the right layout to use, consider a numeric input for a calculator. A numeric input for a calculator might consist of four rows and three columns, each with a button. The following code implements this design:

```xml
<Grid>
  <Grid.RowDefinitions>
    <RowDefinition Height="*" />
    <RowDefinition Height="*" />
    <RowDefinition Height="*" />
    <RowDefinition Height="*" />
  </Grid.RowDefinitions>

  <Grid.ColumnDefinitions>
    <ColumnDefinition Width="*" />
    <ColumnDefinition Width="*" />
    <ColumnDefinition Width="*" />
  </Grid.ColumnDefinitions>
  <Button Text="1" Grid.Row="0" Grid.Column="0" />
  <Button Text="2" Grid.Row="0" Grid.Column="1" />
  <Button Text="3" Grid.Row="0" Grid.Column="2" />
  <Button Text="4" Grid.Row="1" Grid.Column="0" />
  <Button Text="5" Grid.Row="1" Grid.Column="1" />
  <Button Text="6" Grid.Row="1" Grid.Column="2" />
  <Button Text="7" Grid.Row="2" Grid.Column="0" />
  <Button Text="8" Grid.Row="2" Grid.Column="1" />
  <Button Text="9" Grid.Row="2" Grid.Column="2" />
  <Button Text="0" Grid.Row="3" Grid.Column="1" />
  <Button Text="<-" Grid.Row="3" Grid.Column="2" />
</Grid>
```

Note the following aspects of the above code:

- Grids and Columns are explicitly specified, not inferred from the content.
- Height and Width values can be set to star, which means that the Grid will set those values to fill the available space.
- Each button's position is specified by Grid.Row & Grid.Column properties.

### LayoutOptions ###
The LayoutOptions structure can be used to define alignment and expansion for a view, relative to its parent.

### Margin and Padding ###
The Margin and Padding properties control layout behavior when an element is rendered in the user interface.

### Device Orientation ###
Xamarin.Forms and its built-in layouts are capable of handling changes in device orientation. Consider which orientations your app will support, as well as how you'll make use of the space provided in landscape and portrait modes.

### Native Embedding ###
Platform-specific controls can be directly added to a Xamarin.Forms layout. In addition, the layout of custom controls can be overridden in order to correct their measurement API usage.

### Layout for Tablet and Desktop apps ###
iOS, Android, and Windows platforms all support larger screen sizes on tablet devices (as well as laptops and desktops for Windows). Xamarin.Forms lets you optimize your app for larger screens by detecting the device type and either adjusting the page layout, or using a totally different page altogether for larger screens.

### Creating Custom Layouts ###
Custom layouts can also be created when the built-in ones fall short. This page demonstrates how to build a custom WrapLayout control with Xamarin.Forms (presented at Evolve 2016).

### Making Your Choice ###
Be aware that in most cases, more than one layout choice can be used to implement your desired design. When there are multiple valid choices, consider which approach will be the easiest for your situation. Most designs can't be realized with just one layout, so nest layouts as needed to create more complex designs.