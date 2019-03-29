---
title: PS/2 (i8042prt) 驱动程序
description: 本主题介绍 I8042prt、 Microsoft Windows 2000 和更高版本的系统函数的驱动程序的 PS/2 式键盘和鼠标设备的功能。
ms.assetid: BB1046EE-8780-46ED-8CEB-63110643D325
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06c6dffc2bc630b40207d25fac8db7e2e545dad8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567256"
---
# <a name="ps2-i8042prt-driver"></a>PS/2 (i8042prt) 驱动程序


本主题介绍的功能*I8042prt*，Microsoft Windows 2000 和更高版本的系统函数的驱动程序的 PS/2 式键盘和鼠标设备。

I8042prt 实现 I8042prt 服务，其可执行映像将 i8042prt.sys。

I8042prt 的功能包括：

-   PS/2 式键盘和鼠标设备的硬件相关的同时操作。

    键盘和鼠标共享 I/O 端口，但使用不同的中断、 中断服务例程 (ISR) 和 ISR 的调度完成例程。

-   Plug and Play、 电源管理和 WMI

-   旧设备的操作。

-   连接[键盘类服务的回调例程](https://msdn.microsoft.com/library/windows/hardware/ff542274)和一个[鼠标类服务的回调例程](https://msdn.microsoft.com/library/windows/hardware/ff542363)。

    I8042prt 使用类服务回调来将数据从输入的数据缓冲区的 I8042prt 传输到的数据缓冲区的类驱动程序。

-   供应商提供的加法[ **PI8042\_键盘\_初始化\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff543243)键盘设备的回调例程。

    可选的较高级别设备筛选器驱动程序提供的回调例程。

-   供应商提供的加法[ **PI8042\_键盘\_ISR** ](https://msdn.microsoft.com/library/windows/hardware/ff543248)回调例程和自定义[ **PI8042\_鼠标\_ISR** ](https://msdn.microsoft.com/library/windows/hardware/ff543252)回调例程。

    可选的较高级别设备筛选器驱动程序提供这些回调例程。

-   [键盘写入缓冲区请求](https://msdn.microsoft.com/library/windows/hardware/ff541263)并[鼠标写入缓冲区请求](https://msdn.microsoft.com/library/windows/hardware/ff541270)。

    较高级别设备筛选器驱动程序可以使用写入缓冲区请求以将其写入到设备与设备的 ISR 同步和其他读取和写入设备上。

-   [键盘启动信息请求](https://msdn.microsoft.com/library/windows/hardware/ff541257)并[鼠标启动信息请求](https://msdn.microsoft.com/library/windows/hardware/ff541265)。

    启动信息请求将指针传递到较高级别筛选器驱动程序的设备的中断对象。 筛选器驱动程序可以使用中断对象以与设备的 ISR 同步其操作。

-   [I8042prt 回调例程](https://msdn.microsoft.com/library/windows/hardware/ff539965)。

    较高级别设备筛选器驱动程序可以使用设备的 ISR 的上下文中的回调例程编写到设备，并从设备队列数据包。

### <a name="registry-settings-associated-with-the-ps2-driver"></a>使用 PS/2 驱动程序相关联的注册表设置

下面是与 PS/2 端口驱动程序相关联的注册表项的列表。

``` syntax
[Key: HKLM\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters]
```

-   EnableWheelDetection \[REG\_DWORD\] – 确定驱动程序是否尝试进行检测并启用滚轮的鼠标设备上。 某些设备配有鼠标滚轮，以提供快速滚动和其他控件功能，如果应用程序支持。
-   ResendIterations \[REG\_DWORD\] – 指定最多的硬件操作尝试的次数。 如果试验的次数超过了此项的值，Windows 会认为操作已失败。
-   NumberOfButtons \[REG\_DWORD\] – 指定在启动时鼠标端口鼠标上的按钮的数目。 如果在启动时检测到的按钮的数目不正确，您可以通过更改此项的值重写它。
-   KeyboardDataQueueSize \[REG\_DWORD\] – 指定键盘事件数的键盘驱动程序缓冲区。 在计算中非分页的内存池键盘驱动程序的内部缓冲区的大小也使用此项。 若要确定要为缓冲区分配的字节数，系统将键盘的大小\_输入\_KeyboardDataQueueSize 的值的数据结构。
-   PollStatusIterations \[REG\_DWORD\] – 指定最多的系统会验证是否在 i8042 控制器状态收银机上的中断的次数。 如果不能在试验中此项的值指定的次数中验证中断，则忽略中断。
-   PollingIterations \[REG\_DWORD\] -指定 Windows 2000 轮询硬件最大次数。 如果超出此项中指定的试验的次数，Windows 2000 将停止轮询。
-   SampleRate \[REG\_DWORD\] – 指定何种频率 PS/2 驱动程序度量值的特征和 ps/2 鼠标的活动。 该驱动程序使用通过采样收集的信息来优化的鼠标设备的操作。
-   PollingIterationsMaximum \[REG\_DWORD\] – 指定 Windows 2000 轮询在较旧样式在键盘的硬件最大次数。 如果超出此项中指定的试验的次数，则 Windows 将停止轮询。
-   MouseResendStallTime \[REG\_DWORD\] – 确定鼠标驱动程序等待的时间重置的确认 (ACK) 如果重新发送消息返回不确认。 当鼠标驱动程序中断服务例程包括重置时，才使用此项。
-   OverrideKeyboardType \[REG\_DWORD\] – 指定键盘类型。 可以将此项添加到注册表，以更正启动时检测到的键盘类型中的错误。
-   OverrideKeyboardSubtype \[REG\_DWORD\] – 指定依赖于 OEM 的键盘子类型。 可以将此项添加到注册表，以更正启动时检测到的键盘子类型中的错误。

有关详细信息，请参阅：

* https://docs.microsoft.com/windows/desktop/sysinfo/about-the-registry
* https://docs.microsoft.com/windows/desktop/sysinfo/registry-reference 
