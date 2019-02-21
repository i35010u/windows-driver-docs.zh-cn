---
title: Static Driver Verifier 常规工具和技术的限制
description: Static Driver Verifier 常规工具和技术的限制
ms.assetid: d263dee5-2408-4772-96d7-d1895a445fab
keywords:
- 静态驱动程序验证程序 WDK 限制
- StaticDV WDK 限制
- SDV WDK 限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7e5ae2e2ac118888b298e2a9703e91847e08b99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555713"
---
# <a name="static-driver-verifier-general-tool-and-technical-limitations"></a>Static Driver Verifier 常规工具和技术的限制


SDV 具有以下常规限制：

-   SDV 验证一次只有一个驱动程序和驱动程序必须遵循完全验证这些驱动程序模型之一：WDM、 KMDF、 NDIS 或 Storport。 有关支持的驱动程序的详细信息，请参阅[确定驱动程序或库是否支持 Static Driver Verifier](determining-if-static-driver-verifier-supports-your-driver-or-library.md)。

-   不属于上述类别之一的驱动程序将会严重限制可以验证和更有可能在分析过程中失败的规则中。

-   驱动程序项目文件和源代码必须位于本地计算机上。 无法远程验证驱动程序。

-   SDV 使用英语 （美国） 区域设置安装。 因此，依赖于区域设置的元素，例如字符串格式设置，使用英语 （美国） 变体。 SDV 安装在本地化版本的 Windows 非英语 （美国），即使存在此限制。

SDV[验证引擎](verification-engine.md)有技术限制，防止它正确地解释一些驱动程序代码。 具体而言，验证引擎：

-   无法识别，32 位整数被限制为 32 位。 因此，它不检测溢出或下溢错误。

-   确保驱动程序的声明其入口点与**静态**关键字进行正确处理。 但是，若要确保静态入口点，并识别，SDV 所需的更改[Sdv map.h](sdv-map-h.md)静态函数的文件：例如，如果您声明静态入口点：

    ```
    static DRIVER_UNLOAD Unload;
    ```

    Sdv map.h 将不包含的常用条目*有趣\_DriverUnload*。

    ```
    #define fun_DriverUnload Unload
    ```

    相反，你看到出错函数名称：

    ```
      #define fun_DriverUnload sdv_static_function_Unload_1
    ```

    这是必要的因为多个模块可能有一个名为的静态函数*Unload*。 名称改变以避免潜在冲突。

-   不能解释驱动程序调度或驱动程序的回调函数，在其中导出驱动程序具有隐藏驱动程序调度函数的模块定义 (.def) 文件的导出驱动程序中定义。 若要避免此问题，请将驱动程序调度函数添加到模块定义 (.def) 文件的 EXPORTS 部分。

-   不能成功检测函数的角色类型，如果对此函数的以下引用位于不在同一个*编译单元*。

    -   函数的声明。
    -   该函数的定义。
    -   驱动程序入口点或回调函数的函数分配。

    *编译单元*这里的源代码文件的最小集以及其他定义的情况下该源代码文件包含的源文件。

    如果函数角色类型未检测到的 SDV，SDV 将不会验证来自该功能的跟踪。

    例如，如果定义了一个驱动程序 （或实现） [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)文件 mydriver.c 中的函数。 此编译单元 （或任何.h 文件包括该 mydriver.c） 必须包含的函数角色类型声明*EvtDriverDeviceAdd*函数。

-   不会解释结构化的异常处理。 有关**试用 / 除外**语句，SDV 分析受保护的节，如同不会引发异常。 不会分析的表达式或异常处理程序代码。

    ```
    // The try/except statement
    __try 
    {
       // guarded section
    }
    __except ( expression )
    {
       // exception handler
    } 
    ```

    有关**try/finally**语句，SDV 分析受保护的节，然后终止处理程序，因为如果不引发任何异常。

    ```
    // The try/finally statement
    __try {
       // guarded section
    }
    __finally {
       // termination handler
    }
    ```

    两个**试用 / 除外**并**try/finally**语句，将忽略 SDV**保留**语句。

    两个**试用 / 除外**并**try/finally**语句，带跳转**尝试**的阻止防止了分析**除**或**最后**语句。 有关如何重写，以便您可以使用保留语句的信息，请参阅本主题的编译器警告[C6242](https://go.microsoft.com/fwlink/p/?linkid=153317)。

-   将忽略指针算法。 例如，它会丢失某些情况下在指针会递增或递减。 此限制可能导致假负和假正结果。

-   将忽略联合。 在大多数情况下**union**被视为**结构**这可能导致假正或假负。

-   将忽略强制转换操作，因此它将丢失通过该改革解决的错误和通过强制转换导致的错误。 例如，则引擎将假定一个整数，它重新强制转换为一个字符仍具有的整数值。

-   只会初始化是函数指针数组的数组。 SDV 发出警告，并将压缩到的前 1000 个元素的数组初始值设定项。 对于其他数组类型，初始化仅第一个元素。

-   在数组中初始化的对象的构造函数不会调用。 例如，在下面的代码段*x*不获取设置为 10 因为 SDV 不调用构造函数。

    ```
    class A
    {
    public:
        A() {
          x = 10;
        }

        int x;
    };

    void main()
    {
        A a[1];
    }
    ```

-   SDV 不支持构造函数来初始化数组的使用。 例如，在下面的代码段中，P 的构造函数在主函数中不会正确调用，并将不会初始化数组 p2 中的元素：
    ```
    class P
    {
    public:
        P() : x(0) {}
        int x;
    };

    void main()
    {
        P* p1 = new P[1];

        P p2[1] = {P()};
    }
    ```

-   SDV 将忽略预编译标头。 SDV 速度变慢编译将驱动程序的目的只是为了加快编译使用预编译标头。 必须使用预编译标头进行成功编译的驱动程序将使用 SDV 编译。

-   无法推断出某些类型的隐式将通过对调用进行的分配**RtlZeroMemory**或**NdisZeroMemory**。 引擎将执行的最大努力分析来初始化为零，但仅限于时它可以确定其类型的内存。 因此，取决于这些函数来初始化内存的代码可能会产生 false 缺陷沿某些代码路径。

-   不支持将允许它来跟踪手动调度到 KMDF 驱动程序的 I/O 请求的内存模型。 引擎仅支持依赖的框架将传送到 （适用于连续或平行调度） 的驱动程序的 I/O 请求的方法。

-   不支持使用 float 数据类型进行比较。 此技术限制可以产生假负和假正结果。

-   SDV 不支持虚拟继承或虚拟函数。 SDV 不会生成遵循通过虚函数，这可能会丢失，则返回 true 的缺陷导致的代码路径的缺陷。 虚拟继承都被视为常规继承，这可能会导致 false 缺陷或丢失，则返回 true 的缺陷。

 

 





