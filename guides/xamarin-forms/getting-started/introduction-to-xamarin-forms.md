# An Introduction to Xamarin.Forms #
> Getting Started with Cross Platform User Interfaces

Xamarin.Forms is a cross-platform natively backed UI toolkit abstraction that allows developers to easily create user interfaces that can be shared across Android, iOS, Windows, and Windows Phone. The user interfaces are rendered using the native controls of the target platform, allowing Xamarin.Forms applications to retain the appropriate look and feel for each platform. This article provides an introduction to Xamarin.Forms and how to get started writing applications with it.

## Views and Layouts ##
There are four main control groups used to create the user interface of a Xamarin.Forms application.

1. Pages – Xamarin.Forms pages represent cross-platform mobile application screens. For more information about Pages, see [Xamarin.Forms Pages](https://developer.xamarin.com/guides/xamarin-forms/controls/pages/).

2. Layouts – Xamarin.Forms layouts are containers used to compose views into logical structures. For more information about Layouts, see [Xamarin.Forms Layouts](https://developer.xamarin.com/guides/xamarin-forms/controls/layouts/).

3. Views – Xamarin.Forms views are the controls displayed on the user interface, such as labels, buttons, and text entry boxes. For more information about Views, see [Xamarin.Forms Views](https://developer.xamarin.com/guides/xamarin-forms/controls/views/).

4. Cells – Xamarin.Forms cells are specialized elements used for items in a list, and describe how each item in a list should be drawn. For more information about Cells, see [Xamarin.Forms Cells](https://developer.xamarin.com/guides/xamarin-forms/controls/cells/).

At runtime, each control will be mapped to its native equivalent, which is what will be rendered.

Controls are hosted inside of a layout. The StackLayout class, which implements a commonly used layout, will now be examined.

