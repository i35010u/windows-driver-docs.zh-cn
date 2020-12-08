---
title: 用于即插即用串行设备的注册表设置
description: 用于即插即用串行设备的注册表设置
keywords:
- 串行驱动程序 WDK，即插即用设备
- 即插即用串行设备 WDK
- 串行设备 WDK，即插即用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c406a0a41728ddb082da0ec8777d1c6132a4153
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811989"
---
# <a name="registry-settings-for-a-plug-and-play-serial-device"></a>用于即插即用串行设备的注册表设置





本主题介绍串行用作即插即用串行设备的函数驱动程序的注册表设置。 串行还将这些设置用作需要 16550 UART 兼容接口的设备的低级设备筛选器驱动程序。

串行在添加设备时查询这些注册表项值。 如果设备特定的条目值不存在，则串行使用串行服务值。

以下注册表设置位于设备的即插即用注册表项下。

<a href="" id="portname--reg-sz-"></a>**Portvalue** (REG \_ SZ)   
指定设备的名称。 设备的名称通常是 COM <em> &lt; n &gt; ，</em>其中 *&lt; n &gt;* 是安装程序从 [com 端口数据库](com-port-database.md)获取的 com 端口号。 但是，可以将设备设置为任何非空字符串。 如果设备配置为 [COM 端口](configuration-of-com-ports.md)，则串行使用端口名称为设备创建符号链接名称。 **Portvalue** 的默认值为空字符串。

<a href="" id="identifier--reg-sz-"></a>**标识符** (REG \_ SZ)   
指定设备的名称。 提供对 **标识符** 输入值的支持是为了与某些传统 PCMCIA 设备兼容。 **标识符** 的使用已过时，不应与 Microsoft Windows 2000 和更高版本的驱动程序一起使用。 有关说明，请参阅 **portvalue** 条目值。

<a href="" id="multiportdevice--reg-dword-"></a>**MultiportDevice** (REG \_ DWORD)   
指定一个布尔型标志，该标志指示串行端口是否为多端口设备上的设备。 如果 **MultiportDevice** 为0x00000000，则串行端口是单机设备;否则，串行端口位于多端口设备上。 **MultiportDevice** 的默认值为0x00000000。

<a href="" id="portindex--reg-dword-"></a>**PortIndex** (REG \_ DWORD)   
指定多端口设备上串行端口的索引号。 **索引** 条目值指定端口是位图还是索引。 **PortIndex** 的默认值为0x00000000。

<a href="" id="clockrate--reg-dword-"></a>**ClockRate** (REG \_ DWORD)   
指定 UART 时钟速率。 **ClockRate** 的默认值为 1843200 hz。

<a href="" id="indexed--reg-dword-"></a>**索引** (REG \_ DWORD)   
指定一个布尔型标志，该标志指示多端口设备上的端口是 *位图* 设备还是 *索引* 端口。 如果 **索引** 为非零，则为该端口建立索引;否则，端口为位图。 **索引** 与 **PortIndex** 条目值结合使用。 **索引** 的默认值为0x00000000。

<a href="" id="disableport--reg-dword-"></a>**DisablePort** (REG \_ DWORD)   
指定是否禁用设备的布尔型标志。 如果 **DisablePort** 为非零，则串行将禁用该设备;否则，设备处于启用状态。 **DisablePort** 条目值的使用已过时，不应与 Windows 2000 和更高版本的驱动程序一起使用。 Windows 2000 通过设备管理器的 GUI 提供一般的手动方法来启用和禁用设备。 **DisablePort** 的默认值为0x00000000。 请注意，将设备标记为已禁用并不意味着设备不存在。 串行仍将尝试检测已禁用的设备是否存在。 如果将设备指定为禁用，则串行返回状态 \_ 将不会 \_ \_ 响应 **IRP \_ MN \_ 启动 \_ 设备** 请求。 启动请求失败后，即插即用管理器将发送删除请求。

<a href="" id="forcefifoenable--reg-dword-"></a>**ForceFifoEnable** (REG \_ DWORD)   
指定一个布尔型标志，该标志指示是否强制串行使用 FIFOs。 如果 **ForceFifoEnable** 为非零，则将使用 FIFOs，而不管串行能否检测是否存在 FIFOs。 否则，FIFOs 仅在串行检测到它们时使用。 **ForceFifoEnable** 的默认值是为串行服务设置的值。  (串行服务的默认值是0x00000001。 ) 

<a href="" id="rxfifo--reg-dword-"></a>**RxFIFO** (REG \_ DWORD)   
指定接收 FIFO 中触发串行端口中断的字节数。 有关有效值，请参阅 GitHub 上的 [串行驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial) 中的 serial 标头文件中定义的常量。 **RxFIFO** 的默认值是为串行服务设置的值。  (串行服务的默认值为8个字节。 ) 

<a href="" id="txfifo--reg-dword-"></a>**TxFIFO** (REG \_ DWORD)   
指定传输 FIFO 中触发串行设备中断的字节数。 有关有效值，请参阅 GitHub 上的 [串行驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/serial/serial) 中的 serial 标头文件中定义的常量。 **TxFIFO** 的默认值是为串行服务设置的值。  (串行服务的默认值为十四个字节。 ) 

<a href="" id="maskinverted--reg-dword-"></a>**MaskInverted** (REG \_ DWORD)   
指定一个布尔型标志，该标志指示串行设备硬件是否反转中断状态寄存器的内容。 如果 **MaskInverted** 为非零，则会反转中断状态寄存器;否则，中断状态寄存器不会反转。 **MaskInverted** 的默认值为0x00000000。

<a href="" id="serialskipexternalnaming--reg-dword-"></a>**SerialSkipExternalNaming** (REG \_ DWORD)   
指定一个布尔型标志，该标志指示串行是否将设备配置为 [COM 端口](configuration-of-com-ports.md)。 如果将 **SerialSkipExternalNaming** 设置为0x00000000，则串行会将设备配置为 COM 端口;否则，串行不会将设备配置为 COM 端口。 **SerialSkipExternalNaming** 的默认值为0x00000000。 有关串行如何将设备配置为 COM 端口的详细信息，请参阅 [Com 端口的外部命名](external-naming-of-com-ports.md)。

<a href="" id="serialrelinquishpowerpolicy--reg-dword-"></a>**SerialRelinquishPowerPolicy** (REG \_ DWORD)   
指定一个布尔型标志，该标志指示串行是否为串行设备堆栈的电源策略所有者。 如果 **SerialRelinquishPowerPolicy** 为零，则串行是电源策略所有者;否则，串行不是电源策略所有者。 **SerialRelinquishPowerPolicy** 的默认值为0x00000000。

<a href="" id="share-system-interrupt--reg-dword-"></a>**共享系统中断** (REG \_ DWORD)   
布尔型标志，指定是否允许系统共享设备使用的中断。 如果 **共享系统中断** 不为零，则可以共享中断;否则，中断无法共享。 **共享系统中断** 的默认值是为串行服务的 **PermitShare** 条目值设置的值。  (**PermitShare** 的默认服务值为0x00000000。 ) 

<a href="" id="serialioresourcesindex--reg-dword-"></a>**SerialIoResourcesIndex** (REG \_ DWORD)   
指定部分资源描述符的索引，串行使用此描述符来确定设备的串行寄存器集的 i/o 地址。 **SerialIoResourceIndex** 的默认值为0x00000000。

 

 




