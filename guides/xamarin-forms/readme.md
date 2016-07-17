# Xamarin.Forms #
[原文链接](https://developer.xamarin.com/guides/xamarin-forms/)
### Cross-Platform User Interfaces with Xamarin.Forms ###
### 使用Xamarin.Forms实现跨平台的用户界面 ###
Xamarin.Forms is a cross-platform UI toolkit that allows developers to easily create native user interface layouts that can be shared across Android, iOS, and Windows Phone. This section contains the [introduction to Xamarin.Forms](https://developer.xamarin.com/guides/xamarin-forms/getting-started/introduction-to-xamarin-forms/) and [our guides](https://developer.xamarin.com/guides/xamarin-forms/#guides) to help you build Xamarin.Forms apps. You can also [learn more](http://xamarin.com/forms) about its capabilities, try our [samples](https://developer.xamarin.com/samples/xamarin-forms/all/), and browse the [API documentation](https://developer.xamarin.com/api/namespace/Xamarin.Forms/).

Xamarin.Forms是一个跨平台UI工具包，她能让开发人员非常容易的创建出可以在Android,iOS和Windows Phone平台共享的用户界面布局。本章包含Xamarin.Forms的介绍和帮助你构建Xamarin.Forms应用的指南两部分。你同时还能学到更多的Xamarin.Forms技术，尝试一下我们的示例，浏览一下我们的API文档吧。

## Creating Mobile Apps with Xamarin.Forms ##
## 使用Xamarin.Forms创建移动应用 ##
![](https://developer.xamarin.com/guides/xamarin-forms/Images/Cover-Preview-thumb.png)

The first edition of Charles Petzold's book

Creating Mobile Apps with Xamarin.Forms is [available as a free download](https://developer.xamarin.com/guides/xamarin-forms/creating-mobile-apps-xamarin-forms/) to help you get started with Xamarin.Forms!

## Xamarin.Forms for Windows ##
![](https://developer.xamarin.com/guides/xamarin-forms/Images/allhanselman-sml.png)

Check out [Xamarin.Forms running on Windows!](https://developer.xamarin.com/guides/xamarin-forms/platform-features/windows/) Add projects that run on Windows 8.1, Windows Phone 8.1, and the Universal Windows Platform to your existing Xamarin.Forms solutions.

## Is Xamarin.Forms right for your project? ##
## Xamarin.Forms适合你的项目吗？ ##
Xamarin provides two ways to build great, native apps. Xamarin.Forms maximizes code sharing, while Xamarin.iOS and Xamarin.Android provide direct access to platform-specific APIs.

Xamarin提供了两种方式来构建很棒的原生的应用。Xamarin.Forms支持最大化的代码共享，然而Xamarin.iOS和Xamarin.Android只支持直接访问具体平台的API（应用程序接口）。

### Xamarin.Forms is best for: ###
### Xamarin.Forms适用于： ###
![](https://developer.xamarin.com/guides/xamarin-forms/Images/approach-xamarin-forms.svg)

* Data entry apps
* 数据录入应用
* Prototypes and proofs-of-concept
* 原型设计和概念验证
* Apps that require little platform-specific functionality
* 仅对具体平台有少量功能依赖的应用
* Apps where code sharing is more important than custom UI
* 对代码共享代码复用要求高，自定义界面要求低的应用

### Xamarin.iOS & Xamarin.Android are best for ###
### Xamarin.iOS和Xamarin.Android适用于： ###
* Apps that require specialized interactions
* 需要特殊交互的应用
* Apps with highly polished design
* 高品质设计的应用
* Apps that use many platform-specific APIs
* 使用了许多特殊平台API的应用
* Apps where custom UI is more important than code sharing
* 自定义界面的要求高于代码共享的应用

Either way, you'll get fully native apps with [shared business logic](https://developer.xamarin.com/guides/cross-platform/application_fundamentals/building_cross_platform_applications/) using C# and the .NET framework.

无论哪种方式，通过使用C#和.NET框架来共享业务逻辑你将会获得完全的原生应用。

## Xamarin.Forms Developer Guides ##
## Xamarin.Forms开发者指南 ##
The documents in this section show you how to build cross-platform apps using Xamarin.Forms.

本章下面的内容将向你展示如何使用Xamarin.Forms构建跨平台的应用。

### [Getting Started](https://developer.xamarin.com/guides/xamarin-forms/getting-started) ###
### 开始入门 ###
This document introduces the basics of Xamarin.Forms development and covers creating and running your first application, and extending the application to include multiple screens.

这个文档介绍Xamarin.Forms基础开发，包括创建和运行你的第一个程序，并扩展这个程序以包含多种屏幕。

### [Xamarin.Forms Controls Reference](https://developer.xamarin.com/guides/xamarin-forms/controls/) ###
### Xamarin.Forms 控件参考 ###
This document is a quick reference to the UI views that make up the Xamarin.Forms framework, such as [Pages](https://developer.xamarin.com/guides/xamarin-forms/controls/Pages/), [Layouts](https://developer.xamarin.com/guides/xamarin-forms/controls/layouts/), [Views](https://developer.xamarin.com/guides/xamarin-forms/controls/views/) and [Cells](https://developer.xamarin.com/guides/xamarin-forms/controls/cells/).

这个文档是一个快速的用户界面视图参考，它是Xamarin.Forms框架的组成部分，例如页面，布局，视图，和单元格。

### [XMAL](https://developer.xamarin.com/guides/xamarin-forms/xaml/) ###
XMAL is a declarative markup language that can be used to define user interfaces. The user interface is defined in an XML file using the XMAL syntax, while runtime behavior is defined in a separate code-behind file.

XMAL是一种标识定义语言，它能被用于定义用户界面。 用户界面使用XMAL语法被定义在XML文件中，而运行时行为被定义在独立的代码（隐藏/后置）文件中。

### [User Interface](https://developer.xamarin.com/guides/xamarin-forms/user-interface/) ###
Working with Xamarin.Forms user interface controls like ListView, TableView, and WebView.

Xamarin.Forms的用户界面控件，有列表视图，表格视图，和网页视图。

### [Templates](https://developer.xamarin.com/guides/xamarin-forms/templates/) ###
### 模板 ###
Control templates provide the ability to easily theme and re-theme application pages at runtime, while data templates provide the ability to define the presentation of data on supported controls.

控制模板提供了在运行时很容易地设置应用程序页的主题和更换主题的能力，数据模板提供了定义数据展示，在支持的控件上。

### [Behaviors](https://developer.xamarin.com/guides/xamarin-forms/behaviors) ###
### 行为 ###
User interface controls can be easily extended without subclassing by using behaviors to add functionality.

用户界面控件可以被轻易的扩展，不是通过子类化，而是通过行为来添加新功能。

### [Platform Features](https://developer.xamarin.com/guides/xamarin-forms/platform-features/) ###
### 平台特性 ###
Taking advantage of platform-specific features with Xamarin.Forms, such as styling iOS application and incorporating the latest iOS 9 features, and updating Android apps to use Material Design.

利用Xamarin.Forms的平台特性，例如iOS样式的应用程序，包括最新的iOS 9特性，使用重要的设计更新Android应用。

### [Working with...](https://developer.xamarin.com/guides/xamarin-forms/working-with/) ###
### 与哪些一起工作 ###
Working with different aspects of the Xamarin.Forms APIs including [images](https://developer.xamarin.com/guides/xamarin-forms/working-with/images/), [fonts](https://developer.xamarin.com/guides/xamarin-forms/working-with/fonts/) and [files](https://developer.xamarin.com/guides/xamarin-forms/working-with/files/).

与Xamarin.Forms的许多不同方面的APIs一起工作，包括图片API，字体API和文件API。

### [Effects](https://developer.xamarin.com/guides/xamarin-forms/effects/) ###
Effects allow the native controls on each platform to be customized, and are typically used for small styling changes.

效果允许每个平台的原生控件被定制，被用于较小的样式改变。

### [Customizing Controls for Each Platform](https://developer.xamarin.com/guides/xamarin-forms/custom-renderer/) ###
### 为每个平台定制控件 ###
Custom Renders let developers 'override' the default rendering of Xamarin.Forms controls to customize their appearance and behavior on each platform (using native SDKs if desired).

自定义渲染器让开发者重写Xamarin.Forms控件默认的渲染方式，以便自定义他们在每个平台上的外观和行为（使用原生SDKs如果需要）。

### [Accessing Native Features via the DependencyService](https://developer.xamarin.com/guides/xamarin-forms/dependency-service/) ###
### 通过依赖服务访问原生特性 ###
The DependencyService provides a simple locator so that you can code to Interfaces in your shared code and provide platform-specific implementations that are automatically resolved, making it easy to reference platform-specific functionality in Xamarin.Forms.

依赖服务提供一个简单的定位器，以便你能在你的共享代码里编写接口，在每个具体平台提供具体实现能被自动执行到，这个机制让我们在Xamarin.Forms中调用具体平台上的功能非常简单。

### [Publish and Subscribe with MessagingCenter](https://developer.xamarin.com/guides/xamarin-forms/messaging-center/) ###
### 消息中心的发布和订阅 ###
Xamarin.Forms MessagingCenter enables view models and other components to communicate with without having to know anything about each other besides a simple Message Contract.

Xamarin.Forms消息中心能让视图模型和其它组件进行通讯，而且彼此不需要知道任何事情，只需要一个简单的消息约定。

### [Web Services](https://developer.xamarin.com/guides/xamarin-forms/web-services) ###
Xamarin.Forms applications can consume web services implemented using a wide variety of technologies, and this guide will examine how to do this.

Xamarin.Forms应用程序能够使用多种技术来使用Web服务来实现功能，这个指南将告诉你如何去做。

### [Advanced Topics](https://developer.xamarin.com/guides/xamarin-forms/advanced/) ###
### 高级主题 ###
The built-in .NET localization framework can be used to build cross-platform multilingual applications with Xamarin.Forms.

内置的.NET本地化框架和Xamarin.Forms能够用来构建跨平台的多语言应用程序。

### Deployment, Testing, and Metrics ###
### 部署，测试，和度量 ###
Stabilize your Xamarin.Forms app by improving its performance, and by writing UI tests on run in the cloud on hundreds of devices.

使用你的Xamarin.Forms应用稳定，提高他的性能，编写运行在拥有数百种设备的云端上的UI测试。

### [Troubleshooting](https://developer.xamarin.com/guides/xamarin-forms/troubleshooting/) ###
### 故障解决 ###
Common problems and how to resolve them.

通常的问题，以及解决方法。

### [Xamarin.Forms XAML Basics](https://developer.xamarin.com/guides/xamarin-forms/user-interface/xaml-basics/) ###
### Xamarin.Forms XAML 基础 ###
XAML——the eXtensible Application Markup Language——allows developers to define user interfaces in Xamarin.Forms application using markup rather than code. XAML is never required in a Xamarin.Forms program but it is often more succinct than equivalent code, more visually coherent, and potentially toolable.  XAML is particularly well suited for use with the popular MVVM (Model-View-ViewModel) application architecture: XAML defines the View that is linked to ViewModel code through XAML-based data bindings.

XAML——可扩展的程序标记语言——允许开发者在Xamarin.Forms应用程序里使用标记定义用户界面，而不是代码。XAML在Xamarin.Forms编程中不是必需的，但它经常比与其等价的代码更简洁，更形象清晰，是一个非常棒的替代工具。XAML非常方便用于流行的MVVM程序构架：XAML定义视图，视图与视图模型代码通过基于XAML的数据绑定语法来进行连接。

### [API Documentation](https://developer.xamarin.com/api/namespace/Xamarin.Forms/) ###
### API文档 ###
Browse the [API documentation for Xamarin.Forms](https://developer.xamarin.com/api/namespace/Xamarin.Forms/).

### [Samples](https://developer.xamarin.com/samples/xamarin-forms/all/) ###
### 示例 ###
Check out the [sample gallery for Xamarin.Forms](https://developer.xamarin.com/samples/xamarin-forms/all/) or clone directly form [Github](https://github.com/xamarin/xamarin-forms-samples).











