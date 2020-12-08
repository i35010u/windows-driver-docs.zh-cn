---
title: 第三方筛选器驱动程序
description: " (WDK) 的 Microsoft Windows 驱动程序工具包中的示例筛选器驱动程序。"
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d1a58b651284a761785541c813eec76cc73a1d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808859"
---
# <a name="3rd-party-filter-drivers"></a>第三方筛选器驱动程序


本主题介绍 Microsoft Windows 驱动程序工具包 (WDK) 中的以下示例筛选器驱动程序的功能：

-   **Kbfiltr**，一种可选的顶层筛选器驱动程序，适用于即插即用 PS/2 样式键盘设备

-   **Moufiltr**，适用于即插即用 PS/2 样式的鼠标设备的可选一级筛选器驱动程序

Kbfiltr 和 Moufiltr 演示了如何筛选 i/o 请求并添加回调例程，用于修改类服务和 I8042prt 操作的操作。

**注意**   适用于 Windows 2000 和更高版本的终端服务器的设计不支持使用示例键盘和鼠标筛选器驱动程序来筛选远程客户端上物理安装的设备的输入。 安装在终端服务器上的筛选器驱动程序只能用于筛选终端服务器上物理安装的设备中的输入。 这是终端服务器 TermDD.sys 驱动程序处理来自远程客户端的输入的方式的结果。

 

Kbfiltr 和 Moufiltr 支持即插即用和电源管理。

Kbfiltr 提供以下回调例程：

<a href="" id="kbfilter-servicecallback"></a>[**KbFilter \_ ServiceCallback**](/previous-versions/ff542297(v=vs.85))  
键盘筛选器服务回调添加到键盘类服务回调中。 可以配置筛选器服务回调来修改在类驱动程序的数据队列中保存的键盘输入数据。

<a href="" id="kbfilter-isrhook"></a>[**KbFilter \_ IsrHook**](/previous-versions/ff542294(v=vs.85))  
键盘筛选器 ISR 挂钩例程是 I8042prt 为键盘设备支持的 **IsrRoutine** 回调的模板。 可将回调配置为自定义键盘 ISR 的操作。

<a href="" id="kbfilter-initializationroutine"></a>[**KbFilter \_ InitializationRoutine**](/previous-versions/ff542293(v=vs.85))  
键盘筛选器初始化例程是 I8042prt 为键盘设备支持的 **InitializationRoutine** 回调的模板。 此回调可配置为自定义键盘设备的初始化。

Moufiltr 提供以下回调例程：

<a href="" id="moufilter-servicecallback"></a>[**MouFilter \_ ServiceCallback**](/previous-versions/ff542380(v=vs.85))  
鼠标筛选器服务回调将添加到鼠标类服务回调。 可以配置筛选器服务回调来修改在类驱动程序的数据队列中保存的鼠标输入数据。

<a href="" id="moufilter-isrhook"></a>[**MouFilter \_ IsrHook**](/previous-versions/ff542379(v=vs.85))  
鼠标筛选器 ISR 挂钩例程是 **IsrRoutine** 回调的模板，I8042prt 支持鼠标设备。 可将回调配置为自定义该鼠标 ISR 的操作。

## <a name="customize-the-initialization-and-isr-of-a-device"></a>自定义设备的初始化和 ISR


供应商可以提供可选的高级设备筛选器驱动程序，可将以下可选回调添加到 I8042prt 的操作：

<a href="" id="pi8042-keyboard-isr"></a>[**PI8042 \_ 键盘 \_ ISR**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_isr)  
键盘中断服务例程 (ISR) 自定义 I8042prt 键盘 ISR 的操作。 如果 I8042prt 的默认操作已足够，则不需要键盘 ISR 回调。 I8042prt 键盘 ISR 验证键盘中断后，它将调用键盘 ISR 回调。

<a href="" id="pi8042-mouse-isr"></a>[**PI8042 \_ 鼠标 \_ ISR**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_mouse_isr)  
鼠标 ISR 自定义 I8042prt 鼠标 ISR 的操作。 如果 I8042prt 的默认操作已足够，则不需要鼠标 ISR 回叫。 I8042prt 鼠标 ISR 验证鼠标中断后，它将调用鼠标 ISR 回调。

<a href="" id="pi8042-keyboard-initialization-routine"></a>[**PI8042 \_ 键盘 \_ 初始化 \_ 例程**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine)  
键盘初始化回调通过 I8042prt 对键盘设备的默认初始化进行了补充。 I8042prt 在初始化键盘设备时调用此例程。

I8042prt 添加由上层设备筛选器驱动程序提供的回调，方法是使用 [**ioctl \_ 内部 \_ I8042 \_ 挂钩 \_ 键盘**](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_keyboard) 设备请求和 [**ioctl \_ 内部 \_ I8042 \_ 挂钩 \_ 鼠标**](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_mouse) 设备请求。 I8042prt 从设备类驱动程序接收到连接请求后，I8042prt 会将特定于设备的挂钩请求同步发送到设备堆栈的顶部。

筛选器驱动程序接收到挂钩请求后，它将执行以下操作：

-   保存传递给筛选器驱动程序的顶层驱动程序挂钩信息（如果有）。

    挂钩信息包括指向上下文的指针、指向 ISR 回调的指针，以及指向初始化回调的指针，该指针仅在) 的情况下 (初始化回叫。

-   用筛选器驱动程序的挂钩信息替换上层驱动程序挂钩信息。

-   保存 I8042prt 的上下文和筛选器驱动程序回调可以使用的回调指针。

示例筛选器驱动程序（Kbfiltr 和 Moufiltr）提供以下回调例程：

-   [**KbFilter \_IsrHook**](/previous-versions/ff542294(v=vs.85)) 是 PI8042 \_ 键盘 ISR 回调的模板 \_ 。

-   [**KbFilter \_InitializationRoutine**](/previous-versions/ff542293(v=vs.85)) 是 PI8042 \_ 键盘 \_ 初始化例程回调的模板 \_ 。

-   [**MouFilter \_IsrHook**](/previous-versions/ff542379(v=vs.85)) 是 PI8042 \_ 鼠标 ISR 回调的模板 \_ 。

## <a name="synchronize-the-operation-of-a-filter-driver-with-a-devices-isr"></a>将筛选器驱动程序的操作与设备的 ISR 同步


I8042prt 使用 "启动信息请求" 将指向设备中断对象的指针传递到其设备堆栈中的顶层驱动程序。 设备启动后，筛选器驱动程序可以使用中断对象将其操作与中断服务例程同步。 筛选器驱动程序只应在对 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)的调用中使用中断对象。

I8042prt 通过使用 [**ioctl \_ 内部 \_ I8042 \_ 键盘 \_ 启动 \_ 信息**](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_start_information) 请求来处理键盘设备，并使用 [**ioctl \_ 内部 \_ I8042 \_ 鼠标 \_ 启动 \_ 信息**](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_start_information) 请求鼠标设备，将中断对象指针传递到设备堆栈的顶部。 在设备的硬件初始化之后，I8042prt 将启动信息请求同步发送到设备堆栈的顶部。 筛选器驱动程序接收到开始信息请求后，它将保存启动信息并将请求向下传递到设备堆栈中。 I8042prt 完成该请求。

## <a name="synchronize-writes-by-a-filter-driver-to-a-device"></a>将筛选器驱动程序写入同步到设备


若要自定义设备的操作，筛选器驱动程序需要向设备写入控件数据。 筛选器驱动程序必须将写入操作与设备的中断服务例程进行同步，并将其他异步读取或写入操作 (到设备上例如，通过 set 的 "输入符号" 请求或设置的键盘指示器请求) 启动的写入。

I8042prt 支持 [**ioctl \_ 内部 \_ I8042 \_ 键盘 \_ 写入 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_write_buffer) 请求和 [**ioctl \_ 内部 \_ I8042 \_ 鼠标 \_ 写入 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_write_buffer) 请求以实现此目的。 写入缓冲区请求与设备的 ISR 以及读取或写入设备的其他请求同步。

## <a name="i8042prt-callbacks-that-filter-drivers-can-use"></a>筛选器驱动程序可以使用的 I8042prt 回调


I8042prt 支持上层设备筛选器驱动程序可在其 ISR 回调中使用的以下回调：

<a href="" id="pi8042-isr-write-port"></a>[**PI8042 \_ ISR \_ 写入 \_ 端口**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_isr_write_port)  
设备的写入端口回拨将写入设备 ISR 的 i8042 端口。

<a href="" id="pi8042-queue-packet"></a>[**PI8042 \_ 队列 \_ 数据包**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_queue_packet)  
设备的队列数据包回叫将输入数据包的队列排队，以便由设备的 ISR *DPC* 进行处理。

<a href="" id="pi8042-synch-read-port"></a>[**PI8042 \_ 同步 \_ 读取 \_ 端口**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_synch_read_port)  
此回调可用于 [**PI8042 \_ 键盘 \_ 初始化 \_ 例程**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine) 回调。 I8042prt 指定 *ReadPort* 参数中用于 I8042prt 输入到键盘初始化例程的读取端口回调。

<a href="" id="pi8042-synch-write-port"></a>[**PI8042 \_ 同步 \_ 写入 \_ 端口**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_synch_write_port)  
此回调可用于 [**PI8042 \_ 键盘 \_ 初始化 \_ 例程**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine) 回调。 I8042prt 指定 *WritePort* 参数中用于 I8042prt 输入到键盘初始化例程的写入端口回调。

I8042prt 将指针传递到在 I8042prt 用于通过 [**IOCTL \_ 内部 \_ I8042 \_ 挂钩 \_ 键盘**](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_keyboard)请求输入信息的 [**内部 \_ I8042 \_ 挂钩 \_ 键盘**](/windows-hardware/drivers/ddi/ntdd8042/ns-ntdd8042-_internal_i8042_hook_keyboard)结构中的键盘设备回调。

I8042prt 在 [**内部 \_ I8042 \_ 挂钩 \_ 鼠标**](/windows-hardware/drivers/ddi/ntdd8042/ns-ntdd8042-_internal_i8042_hook_mouse) 结构中传递指向鼠标设备回调的指针，I8042prt 使用该指针通过 [**IOCTL \_ 内部 \_ I8042 \_ 挂钩 \_ 键盘**](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_hook_keyboard) 请求输入信息。

筛选器驱动程序接收到挂钩设备请求后，它会保存用于筛选器驱动程序的 ISR 回调中的 I8042prt 回调指针。

 

