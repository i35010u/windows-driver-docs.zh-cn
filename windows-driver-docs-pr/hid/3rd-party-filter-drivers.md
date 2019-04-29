---
title: 第三方筛选器驱动程序
ms.assetid: 2EAFE726-2266-4E40-AC51-0025BF6069B6
description: 示例筛选器驱动程序中 Microsoft Windows Driver Kit (WDK)。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 763eb9aa7503a66938bdee9dddefde5e806c5cf1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390406"
---
# <a name="3rd-party-filter-drivers"></a>第三方筛选器驱动程序


本主题介绍以下示例筛选器驱动程序中 Microsoft Windows Driver Kit (WDK) 的功能：

-   **Kbfiltr**，插 PS/2-样式键盘设备的可选较高级别筛选器驱动程序

-   **Moufiltr**，插 PS/2-样式鼠标设备的可选较高级别筛选器驱动程序

Kbfiltr 和 Moufiltr 演示如何筛选 I/O 请求并添加修改类服务的操作和 I8042prt 操作的回调例程。

**请注意**  设计的终端服务器的 Windows 2000 及更高版本不支持使用示例键盘和鼠标筛选器驱动程序来进行筛选来自远程客户端上以物理方式安装的设备的输入。 在终端服务器上安装了筛选器驱动程序仅用于筛选以物理方式安装在终端服务器上的设备的输入。 这是方式的终端服务器的 TermDD.sys 驱动程序处理来自远程客户端输入的结果。

 

Kbfiltr 和 Moufiltr 支持插和电源管理。

Kbfiltr 提供了以下回调例程：

<a href="" id="kbfilter-servicecallback"></a>[**KbFilter\_ServiceCallback**](https://msdn.microsoft.com/library/windows/hardware/ff542297)  
键盘筛选器服务回调添加到键盘类服务回调。 筛选器服务回调可以进行配置以修改键盘输入的数据保存在类驱动程序的数据队列中。

<a href="" id="kbfilter-isrhook"></a>[**KbFilter\_IsrHook**](https://msdn.microsoft.com/library/windows/hardware/ff542294)  
键盘筛选器 ISR 挂钩例程是一个模板，用于**IsrRoutine** I8042prt 支持键盘的设备的回调。 回调可以配置为自定义键盘 ISR 的操作。

<a href="" id="kbfilter-initializationroutine"></a>[**KbFilter\_InitializationRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff542293)  
键盘筛选器初始化例程是一个模板，用于**InitializationRoutine** I8042prt 支持键盘的设备的回调。 此回调可以配置为自定义的键盘设备初始化。

Moufiltr 提供了以下回调例程：

<a href="" id="moufilter-servicecallback"></a>[**MouFilter\_ServiceCallback**](https://msdn.microsoft.com/library/windows/hardware/ff542380)  
鼠标筛选器服务回调添加到鼠标类服务回调。 筛选器服务回调可以配置为修改的类驱动程序的数据队列中保存的鼠标输入的数据。

<a href="" id="moufilter-isrhook"></a>[**MouFilter\_IsrHook**](https://msdn.microsoft.com/library/windows/hardware/ff542379)  
鼠标筛选器 ISR 挂钩例程是一个模板，用于**IsrRoutine** I8042prt 鼠标的设备支持的回调。 回调可以配置为自定义该鼠标 ISR.操作

## <a name="customize-the-initialization-and-isr-of-a-device"></a>自定义初始化和 ISR 的设备


供应商可以提供可选的较高级别设备筛选器驱动程序，可将以下可选回调添加到 I8042prt 操作：

<a href="" id="pi8042-keyboard-isr"></a>[**PI8042\_键盘\_ISR**](https://msdn.microsoft.com/library/windows/hardware/ff543248)  
键盘中断服务例程 (ISR) 自定义 I8042prt 键盘 ISR.的操作 如果 I8042prt 的默认操作是足够，则不需要键盘 ISR 回调。 I8042prt 键盘 ISR 验证键盘中断后，它会调用键盘 ISR 回调。

<a href="" id="pi8042-mouse-isr"></a>[**PI8042\_MOUSE\_ISR**](https://msdn.microsoft.com/library/windows/hardware/ff543252)  
鼠标 ISR 自定义 I8042prt 鼠标 ISR.的操作 如果 I8042prt 的默认操作是足够，则不需要鼠标 ISR 回调。 I8042prt 鼠标 ISR 验证鼠标中断后，它会调用鼠标 ISR 回调。

<a href="" id="pi8042-keyboard-initialization-routine"></a>[**PI8042\_键盘\_初始化\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff543243)  
键盘初始化回调补充由 I8042prt 键盘设备的默认初始化。 I8042prt 调用此例程时初始化键盘设备。

I8042prt 添加通过使用由较高级别设备筛选器驱动程序提供的回叫[ **IOCTL\_内部\_I8042\_挂钩\_键盘**](https://msdn.microsoft.com/library/windows/hardware/ff541233)键盘设备的请求和一个[ **IOCTL\_内部\_I8042\_挂钩\_鼠标**](https://msdn.microsoft.com/library/windows/hardware/ff541242)鼠标设备的请求。 I8042prt 从设备类驱动程序收到连接请求后，I8042prt 以同步方式将特定于设备的挂钩请求发送到设备堆栈的顶部。

筛选器驱动程序收到挂钩请求后，执行以下操作：

-   如果任何传递给筛选器驱动程序会保存别的驱动程序挂钩信息。

    挂钩信息包括到上下文的指针、 ISR 回调指针和指向的初始化回调 （键盘仅初始化回调） 的指针。

-   使用筛选器驱动程序的挂钩信息替换较高级别驱动程序挂钩信息。

-   将上下文 I8042prt 和指针保存到可以使用筛选器驱动程序回调的回调。

示例筛选器驱动程序，Kbfiltr 和 Moufiltr，提供以下回调例程：

-   [**KbFilter\_IsrHook** ](https://msdn.microsoft.com/library/windows/hardware/ff542294)是一个模板用于 PI8042\_键盘\_ISR 回调。

-   [**KbFilter\_InitializationRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff542293)是一个模板用于 PI8042\_键盘\_初始化\_例程回调。

-   [**MouFilter\_IsrHook** ](https://msdn.microsoft.com/library/windows/hardware/ff542379)是一个模板用于 PI8042\_鼠标\_ISR 回调。

## <a name="synchronize-the-operation-of-a-filter-driver-with-a-devices-isr"></a>与设备的 ISR 同步筛选器驱动程序的操作


I8042prt 使用启动信息请求将指针传递到设备的中断对象及其设备堆栈中的较高级别驱动程序。 启动设备后，筛选器驱动程序可用于中断对象同步其操作与中断服务例程。 筛选器驱动程序应仅对的调用中使用的中断对象[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)。

I8042prt 将中断对象指针通过使用设备堆栈的顶部[ **IOCTL\_内部\_I8042\_键盘\_启动\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff541257)键盘设备的请求和一个[ **IOCTL\_内部\_I8042\_鼠标\_启动\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff541265)鼠标设备的请求。 I8042prt 以同步方式将设备的硬件初始化后启动信息请求发送到设备堆栈的顶部。 筛选器驱动程序收到一个开始信息请求后，它将保存启动信息，并将传递设备堆栈请求。 I8042prt 完成请求。

## <a name="synchronize-writes-by-a-filter-driver-to-a-device"></a>同步写入到设备的筛选器驱动程序


若要自定义设备的操作，筛选器驱动程序需要将控件数据写入到设备。 筛选器驱动程序必须与设备的中断服务例程同步到设备的写入和其他异步读取或写入设备 （例如，由集字符重复请求或 set 键盘指示器请求启动的写入） 上。

支持 I8042prt [ **IOCTL\_内部\_I8042\_键盘\_编写\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff541263)请求和[**IOCTL\_内部\_I8042\_鼠标\_编写\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff541270)实现此目的的请求。 写入缓冲区请求与设备的 ISR 和其他请求的读取或写入该设备进行同步。

## <a name="i8042prt-callbacks-that-filter-drivers-can-use"></a>可以使用筛选器驱动程序的 I8042prt 回调


I8042prt 支持其 ISR 回调中较高级别设备筛选器驱动程序可以使用以下回调：

<a href="" id="pi8042-isr-write-port"></a>[**PI8042\_ISR\_WRITE\_PORT**](https://msdn.microsoft.com/library/windows/hardware/ff543231)  
设备的写入端口回调将写入到的设备的 ISR.IRQL i8042 端口

<a href="" id="pi8042-queue-packet"></a>[**PI8042\_QUEUE\_PACKET**](https://msdn.microsoft.com/library/windows/hardware/ff543263)  
设备的队列数据包回调排队供设备的 ISR 处理的输入的数据数据包*DPC*。

<a href="" id="pi8042-synch-read-port"></a>[**PI8042\_SYNCH\_READ\_PORT**](https://msdn.microsoft.com/library/windows/hardware/ff543272)  
可以在使用此回叫[ **PI8042\_键盘\_初始化\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff543243)回调。 I8042prt 指定在读取的端口回调*ReadPort*参数该 I8042prt 输入到键盘初始化例程。

<a href="" id="pi8042-synch-write-port"></a>[**PI8042\_SYNCH\_WRITE\_PORT**](https://msdn.microsoft.com/library/windows/hardware/ff543276)  
可以在使用此回叫[ **PI8042\_键盘\_初始化\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff543243)回调。 I8042prt 指定中的写入端口回调*WritePort*参数该 I8042prt 输入到键盘初始化例程。

I8042prt 将指针传递给键盘设备回调[**内部\_I8042\_挂钩\_键盘**](https://msdn.microsoft.com/library/windows/hardware/ff541039) I8042prt 用于输入信息的结构与[ **IOCTL\_内部\_I8042\_挂钩\_键盘**](https://msdn.microsoft.com/library/windows/hardware/ff541233)请求。

I8042prt 将指针传递给鼠标设备回调[**内部\_I8042\_挂钩\_鼠标**](https://msdn.microsoft.com/library/windows/hardware/ff541044) I8042prt 用于输入信息的结构[ **IOCTL\_内部\_I8042\_挂钩\_键盘**](https://msdn.microsoft.com/library/windows/hardware/ff541233)请求。

筛选器驱动程序收到挂钩设备请求后，它将使用 I8042prt 回调指针保存在筛选器驱动程序的 ISR 回调。

 

 




