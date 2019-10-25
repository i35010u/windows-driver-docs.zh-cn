---
title: 第三方筛选器驱动程序
ms.assetid: 2EAFE726-2266-4E40-AC51-0025BF6069B6
description: Microsoft Windows 驱动程序工具包（WDK）中的示例筛选器驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 044843853336f840c598371c5fd156c63be0288e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824883"
---
# <a name="3rd-party-filter-drivers"></a>第三方筛选器驱动程序


本主题介绍 Microsoft Windows 驱动程序工具包（WDK）中的以下示例筛选器驱动程序的功能：

-   **Kbfiltr**，一种可选的顶层筛选器驱动程序，适用于即插即用 PS/2 样式键盘设备

-   **Moufiltr**，适用于即插即用 PS/2 样式的鼠标设备的可选一级筛选器驱动程序

Kbfiltr 和 Moufiltr 演示了如何筛选 i/o 请求并添加回调例程，用于修改类服务和 I8042prt 操作的操作。

**请注意**   适用于 Windows 2000 和更高版本的终端服务器的设计不支持使用示例键盘和鼠标筛选器驱动程序来筛选远程客户端上物理安装的设备的输入。 安装在终端服务器上的筛选器驱动程序只能用于筛选终端服务器上物理安装的设备中的输入。 这是终端服务器的 Termdd.sys 驱动程序处理来自远程客户端的输入的一种结果。

 

Kbfiltr 和 Moufiltr 支持即插即用和电源管理。

Kbfiltr 提供以下回调例程：

<a href="" id="kbfilter-servicecallback"></a>[**KbFilter\_ServiceCallback**](https://docs.microsoft.com/previous-versions/ff542297(v=vs.85))  
键盘筛选器服务回调添加到键盘类服务回调中。 可以配置筛选器服务回调来修改在类驱动程序的数据队列中保存的键盘输入数据。

<a href="" id="kbfilter-isrhook"></a>[**KbFilter\_IsrHook**](https://docs.microsoft.com/previous-versions/ff542294(v=vs.85))  
键盘筛选器 ISR 挂钩例程是 I8042prt 为键盘设备支持的**IsrRoutine**回调的模板。 可将回调配置为自定义键盘 ISR 的操作。

<a href="" id="kbfilter-initializationroutine"></a>[**KbFilter\_InitializationRoutine**](https://docs.microsoft.com/previous-versions/ff542293(v=vs.85))  
键盘筛选器初始化例程是 I8042prt 为键盘设备支持的**InitializationRoutine**回调的模板。 此回调可配置为自定义键盘设备的初始化。

Moufiltr 提供以下回调例程：

<a href="" id="moufilter-servicecallback"></a>[**MouFilter\_ServiceCallback**](https://docs.microsoft.com/previous-versions/ff542380(v=vs.85))  
鼠标筛选器服务回调将添加到鼠标类服务回调。 可以配置筛选器服务回调来修改在类驱动程序的数据队列中保存的鼠标输入数据。

<a href="" id="moufilter-isrhook"></a>[**MouFilter\_IsrHook**](https://docs.microsoft.com/previous-versions/ff542379(v=vs.85))  
鼠标筛选器 ISR 挂钩例程是**IsrRoutine**回调的模板，I8042prt 支持鼠标设备。 可将回调配置为自定义该鼠标 ISR 的操作。

## <a name="customize-the-initialization-and-isr-of-a-device"></a>自定义设备的初始化和 ISR


供应商可以提供可选的高级设备筛选器驱动程序，可将以下可选回调添加到 I8042prt 的操作：

<a href="" id="pi8042-keyboard-isr"></a>[**PI8042\_键盘\_ISR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_isr)  
键盘中断服务例程（ISR）自定义 I8042prt 键盘 ISR 的操作。 如果 I8042prt 的默认操作已足够，则不需要键盘 ISR 回调。 I8042prt 键盘 ISR 验证键盘中断后，它将调用键盘 ISR 回调。

<a href="" id="pi8042-mouse-isr"></a>[**PI8042\_鼠标\_ISR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_mouse_isr)  
鼠标 ISR 自定义 I8042prt 鼠标 ISR 的操作。 如果 I8042prt 的默认操作已足够，则不需要鼠标 ISR 回叫。 I8042prt 鼠标 ISR 验证鼠标中断后，它将调用鼠标 ISR 回调。

<a href="" id="pi8042-keyboard-initialization-routine"></a>[**PI8042\_键盘\_初始化\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine)  
键盘初始化回调通过 I8042prt 对键盘设备的默认初始化进行了补充。 I8042prt 在初始化键盘设备时调用此例程。

I8042prt 通过使用[**IOCTL\_内部\_I8042\_挂钩\_键盘**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_keyboard)设备的键盘请求和[**ioctl\_内部\_I8042，来添加由上层设备筛选器驱动程序提供的回调\_挂钩\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_mouse)鼠标设备的鼠标请求。 I8042prt 从设备类驱动程序接收到连接请求后，I8042prt 会将特定于设备的挂钩请求同步发送到设备堆栈的顶部。

筛选器驱动程序接收到挂钩请求后，它将执行以下操作：

-   保存传递给筛选器驱动程序的顶层驱动程序挂钩信息（如果有）。

    挂钩信息包括指向上下文的指针、指向 ISR 回调的指针和指向初始化回调（仅针对键盘的初始化回叫）的指针。

-   用筛选器驱动程序的挂钩信息替换上层驱动程序挂钩信息。

-   保存 I8042prt 的上下文和筛选器驱动程序回调可以使用的回调指针。

示例筛选器驱动程序（Kbfiltr 和 Moufiltr）提供以下回调例程：

-   [**KbFilter\_IsrHook**](https://docs.microsoft.com/previous-versions/ff542294(v=vs.85))是 PI8042\_键盘\_ISR 回叫的模板。

-   [**KbFilter\_InitializationRoutine**](https://docs.microsoft.com/previous-versions/ff542293(v=vs.85))是 PI8042\_键盘的一个模板，\_初始化\_例程回调。

-   [**MouFilter\_IsrHook**](https://docs.microsoft.com/previous-versions/ff542379(v=vs.85))是 PI8042\_鼠标\_ISR 回叫的模板。

## <a name="synchronize-the-operation-of-a-filter-driver-with-a-devices-isr"></a>将筛选器驱动程序的操作与设备的 ISR 同步


I8042prt 使用 "启动信息请求" 将指向设备中断对象的指针传递到其设备堆栈中的顶层驱动程序。 设备启动后，筛选器驱动程序可以使用中断对象将其操作与中断服务例程同步。 筛选器驱动程序只应在对[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)的调用中使用中断对象。

I8042prt 通过使用[**IOCTL\_内部\_I8042\_键盘**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_start_information)，将中断对象指针传递到设备堆栈的顶部\_启动键盘设备\_信息请求和[**ioctl\_内部\_I8042\_鼠标\_开始\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_start_information)请求鼠标设备。 在设备的硬件初始化之后，I8042prt 将启动信息请求同步发送到设备堆栈的顶部。 筛选器驱动程序接收到开始信息请求后，它将保存启动信息并将请求向下传递到设备堆栈中。 I8042prt 完成该请求。

## <a name="synchronize-writes-by-a-filter-driver-to-a-device"></a>将筛选器驱动程序写入同步到设备


若要自定义设备的操作，筛选器驱动程序需要向设备写入控件数据。 筛选器驱动程序必须将对设备的写入与设备的中断服务例程以及设备上的其他异步读取或写入（例如，由 set 按键请求或设置的键盘指示器请求启动的写入）进行同步。

I8042prt 支持[**IOCTL\_内部\_I8042\_键盘\_编写\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_write_buffer)请求和[**ioctl\_内部\_I8042\_鼠标\_写入\_的缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_write_buffer)请求此目的。 写入缓冲区请求与设备的 ISR 以及读取或写入设备的其他请求同步。

## <a name="i8042prt-callbacks-that-filter-drivers-can-use"></a>筛选器驱动程序可以使用的 I8042prt 回调


I8042prt 支持上层设备筛选器驱动程序可在其 ISR 回调中使用的以下回调：

<a href="" id="pi8042-isr-write-port"></a>[**PI8042\_ISR\_写入\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_isr_write_port)  
设备的写入端口回拨将写入设备 ISR 的 i8042 端口。

<a href="" id="pi8042-queue-packet"></a>[**PI8042\_队列\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_queue_packet)  
设备的队列数据包回叫将输入数据包的队列排队，以便由设备的 ISR *DPC*进行处理。

<a href="" id="pi8042-synch-read-port"></a>[**PI8042\_同步\_读取\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_synch_read_port)  
此回调可用于[**PI8042\_键盘\_初始化\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine)回调。 I8042prt 指定*ReadPort*参数中用于 I8042prt 输入到键盘初始化例程的读取端口回调。

<a href="" id="pi8042-synch-write-port"></a>[**PI8042\_同步\_写入\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_synch_write_port)  
此回调可用于[**PI8042\_键盘\_初始化\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine)回调。 I8042prt 指定*WritePort*参数中用于 I8042prt 输入到键盘初始化例程的写入端口回调。

I8042prt 在[**内部\_I8042\_挂钩\_键盘**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ns-ntdd8042-_internal_i8042_hook_keyboard)结构中传递指向键盘设备回调的指针，I8042prt 使用该指针通过[**IOCTL\_内部\_I8042\_挂钩来输入信息\_键盘**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_keyboard)请求。

I8042prt 将指针传递到[**内部\_I8042\_挂钩\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ns-ntdd8042-_internal_i8042_hook_mouse)鼠标结构中的鼠标设备回调鼠标结构，I8042prt 使用该指针通过[**IOCTL\_内部\_I8042\_挂钩来输入信息\_键盘**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_keyboard)请求。

筛选器驱动程序接收到挂钩设备请求后，它会保存用于筛选器驱动程序的 ISR 回调中的 I8042prt 回调指针。

 

 




