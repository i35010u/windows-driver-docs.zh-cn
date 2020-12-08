---
title: 静态驱动程序验证程序常规工具和技术限制
description: 静态驱动程序验证程序常规工具和技术限制
keywords:
- 静态驱动程序验证程序 WDK，限制
- StaticDV WDK，限制
- SDV WDK，限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5101e57bf546312b77f4fb9f962b522900e27cf9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799751"
---
# <a name="static-driver-verifier-general-tool-and-technical-limitations"></a>静态驱动程序验证程序常规工具和技术限制


SDV 具有以下一般限制：

-   SDV 一次只验证一个驱动程序，并且驱动程序必须遵循下列驱动程序模型之一来进行完全验证： WDM、KMDF、NDIS 或 Storport。 有关支持的驱动程序的详细信息，请参阅 [确定 Static Driver Verifier 是否支持驱动程序或库](determining-if-static-driver-verifier-supports-your-driver-or-library.md)。

-   对于不属于上述某个类别的驱动程序，可验证的规则会受到严重限制，在分析过程中更有可能会失败。

-   驱动程序项目文件和源代码必须位于本地计算机上。 不能远程验证驱动程序。

-   SDV 随英语 (美国) 区域设置一起安装。 因此，与区域设置相关的元素（如字符串格式设置）使用英语 (美国) 变体。 即使在非英语 (美国) 上安装了 SDV，也存在此限制。

SDV [验证引擎](verification-engine.md) 具有可防止其正确解释某些驱动程序代码的技术限制。 具体而言，验证引擎：

-   无法识别32位整数限制为32位。 因此，它不检测溢出或下溢错误。

-   确保正确处理用 **static** 关键字声明其入口点的驱动程序。 但是，若要确保识别静态入口点，SDV 需要更改静态函数的 [SDV](sdv-map-h.md) 文件：例如，如果声明静态入口点：

    ```
    static DRIVER_UNLOAD Unload;
    ```

    Sdv 不会包含 *有趣 \_ DriverUnload* 的常用条目。

    ```
    #define fun_DriverUnload Unload
    ```

    相反，您会看到函数名称出错：

    ```
      #define fun_DriverUnload sdv_static_function_Unload_1
    ```

    这是必需的，因为多个模块可能具有名为 *Unload* 的静态函数。 名称有可能会导致潜在的冲突。

-   无法解释在导出驱动程序中定义的驱动程序调度或驱动程序回调函数，其中，导出驱动程序的模块定义 ( .def 隐藏驱动程序调度函数) 文件。 若要避免此问题，请将驱动程序调度函数添加到模块定义 ( .def) 文件的导出部分。

-   如果对此函数的以下引用不在同一 *编译单元* 中，则无法成功检测函数的角色类型。

    -   函数的声明。
    -   函数的定义。
    -   将函数分配给驱动程序入口点或回调函数。

    *编译单元* 定义为此源代码文件所包含的一组最小的源代码文件和其他源文件。

    如果 SDV 未检测到函数角色类型，则 SDV 将不会验证源自此函数的跟踪。

    例如，如果驱动程序定义 (或实现) 文件 mydriver 中的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 函数。 此编译单元 (或 mydriver 包含) 必须包含 *EvtDriverDeviceAdd* 函数的函数角色类型声明的所有 .h 文件。

-   不解释结构化异常处理。 对于 **try/except** 语句，SDV 将分析受保护的节，就好像未引发异常一样。 不分析表达式或异常处理程序代码。

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

    对于 **try/finally** 语句，SDV 将分析受保护的部分，然后分析终止处理程序，就像未引发异常一样。

    ```
    // The try/finally statement
    __try {
       // guarded section
    }
    __finally {
       // termination handler
    }
    ```

    对于 **try/except** 和 **try/FINALLY** 语句，SDV **将忽略 leave** 语句。

    对于 **try/except** 和 **try/finally** 语句， **try** 块的跳出会阻止分析 **except** 或 **finally** 语句。 有关如何重写以便可以使用 leave 语句的信息，请参阅有关编译器警告的主题 [C6242](/cpp/code-quality/c6242)。

-   忽略指针算法。 例如，它会遗漏指针递增或递减的情况。 此限制可能导致误报和误报结果。

-   忽略联合。 在大多数情况下， **union** 被视为 **结构** ，这可能会导致误报或误报。

-   忽略强制转换操作，因此它将丢失由 recasting 解决的错误和由强制转换导致的错误。 例如，引擎假设作为字符重塑的整数仍包含整数值。

-   仅初始化作为函数指针数组的数组。 SDV 会发出警告，并将数组初始值设定项压缩为前1000个元素。 对于其他数组类型，只初始化第一个元素。

-   不会调用在数组中初始化的对象的构造函数。 例如，在以下代码片段中， *x* 不会设置为10，因为 SDV 不会调用构造函数。

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

-   SDV 不支持使用构造函数来初始化数组。 例如，在以下代码片段中，P 的构造函数在 main 函数中将不会正确调用，并且将不会初始化数组 p2 中的元素：
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

-   SDV 将忽略预编译头。 将预编译标头仅用于加速编译的驱动程序将使用 SDV 进行编译。 必须使用预编译头才能成功编译的驱动程序将不会使用 SDV 进行编译。

-   无法推导通过调用 **RtlZeroMemory** 或 **NdisZeroMemory** 进行的某些类型的隐式赋值。 引擎执行尽力分析以将内存初始化为零，但只能在它可以识别其类型时进行分析。 因此，依赖于这些函数初始化内存的代码可能会在某些代码路径中产生错误。

-   不支持内存模型，使其能够跟踪对 KMDF 驱动程序的 i/o 请求的手动分派。 引擎仅支持依赖于框架的方法将 i/o 请求传递到 (顺序或并行调度) 的驱动程序中。

-   不支持使用 float 数据类型进行比较。 这种技术限制可能产生误报和误报结果。

-   SDV 不支持虚拟继承或虚函数。 SDV 不会通过虚函数生成遵循代码路径的缺陷，这可能会导致丢失真实缺陷。 虚拟继承的处理方式类似于常规继承，这可能会导致错误或丢失真实缺陷。

 

