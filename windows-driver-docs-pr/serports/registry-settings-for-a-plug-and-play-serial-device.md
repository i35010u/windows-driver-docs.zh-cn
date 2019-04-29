---
title: 用于即插即用串行设备的注册表设置
description: 用于即插即用串行设备的注册表设置
ms.assetid: 57bd090a-20fe-41c6-b730-0479f6ae0982
keywords:
- 串行驱动程序 WDK，插设备
- 即插即用串行设备 WDK
- 串行设备 WDK，插
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e60723543d8165daf522242b232913250b8ea986
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382552"
---
# <a name="registry-settings-for-a-plug-and-play-serial-device"></a>用于即插即用串行设备的注册表设置





本主题介绍序列插串行设备使用作为功能驱动程序的注册表设置。 设备需要 16550 UART 兼容接口序列作为较低级别设备筛选器驱动程序还使用这些设置。

当添加设备时，序列查询这些注册表项值。 如果不存在特定于设备的条目值，序列将使用串行服务值。

以下注册表设置将设备插注册表项下。

<a href="" id="portname--reg-sz-"></a>**PortName** (REG\_SZ)  
指定的设备的名称。 设备的名称通常是 COM<em>&lt;n&gt;，</em>其中*&lt;n&gt;* 是从安装程序获取 COM 端口号[COM端口数据库](com-port-database.md)。 但是，设备可以设置为任何非 NULL 字符串。 如果设备被配置为[COM 端口](configuration-of-com-ports.md)，序列使用的端口名称来创建设备的符号链接名称。 默认值**PortName**为空字符串。

<a href="" id="identifier--reg-sz-"></a>**标识符**(REG\_SZ)  
指定的设备的名称。 为支持**标识符**条目值，提供与某些旧的 PCMCIA 设备的兼容性。 利用**标识符**已过时，不能与 Microsoft Windows 2000 和更高版本的驱动程序。 有关说明，请参阅**PortName**条目值。

<a href="" id="multiportdevice--reg-dword-"></a>**MultiportDevice** (REG\_DWORD)  
指定一个布尔标志，指示串行端口是否为多个端口的设备上的设备。 如果**MultiportDevice**为 0x00000000，串行端口是独立的设备; 否则，串行端口是多端口设备上。 默认值**MultiportDevice**为 0x00000000。

<a href="" id="portindex--reg-dword-"></a>**PortIndex** (REG\_DWORD)  
多端口设备上指定的串行端口的编号。 **索引**条目值，指定一个端口是位图化或索引。 默认值**PortIndex**为 0x00000000。

<a href="" id="clockrate--reg-dword-"></a>**ClockRate** (REG\_DWORD)  
指定 UART 时钟速度。 默认值**ClockRate**是 1,843,200 赫兹。

<a href="" id="indexed--reg-dword-"></a>**Indexed** (REG\_DWORD)  
指定一个布尔标志，指示多端口设备上的某个端口是否*位图*或*索引*。 如果**索引**为非零值，该端口编制索引的索引; 否则，该端口是位图化。 **编制索引**结合使用**PortIndex**条目值。 默认值**索引**为 0x00000000。

<a href="" id="disableport--reg-dword-"></a>**DisablePort** (REG\_DWORD)  
布尔标志，指定是否要禁用设备。 如果**DisablePort**是禁用的非零值，序列的设备; 否则，启用设备。 利用**DisablePort**条目值已过时，不能与 Windows 2000 和更高版本的驱动程序。 Windows 2000 提供了通用的手动方法通过 GUI 的设备管理器来启用和禁用设备。 默认值**DisablePort**为 0x00000000。 请注意，将设备标记为已禁用并不意味着设备不存在。 序列仍尝试检测存在被禁用的设备。 如果为已禁用指定设备，则序列将返回状态\_否\_SUCH\_设备响应**IRP\_MN\_启动\_设备**请求。 启动请求失败后，插 manager 将发送的删除请求。

<a href="" id="forcefifoenable--reg-dword-"></a>**ForceFifoEnable** (REG\_DWORD)  
指定一个布尔标志，指示是否强制使用 FIFOs 的序列。 如果**ForceFifoEnable**为非零值，FIFOs 习惯，而不考虑是否序列可以检测 FIFOs 的状态。 否则，如果序列可以检测到它们，仅使用 FIFOs。 默认值**ForceFifoEnable**是串行服务设置的值。 （串行服务默认值为 0x00000001。）

<a href="" id="rxfifo--reg-dword-"></a>**RxFIFO** (REG\_DWORD)  
在接收触发串口中断的先进先出指定字节的数。 有关有效的值，请参阅 Serial.h 标头文件中定义的常量[串行驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub 上。 默认值**RxFIFO**是串行服务设置的值。 （串行服务的默认值为 8 个字节。）

<a href="" id="txfifo--reg-dword-"></a>**TxFIFO** (REG\_DWORD)  
指定在传输触发串行设备中断的先进先出的字节数。 有关有效的值，请参阅 Serial.h 标头文件中定义的常量[串行驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617962)GitHub 上。 默认值**TxFIFO**是串行服务设置的值。 （串行服务的默认值为 14 个字节。）

<a href="" id="maskinverted--reg-dword-"></a>**MaskInverted** (REG\_DWORD)  
指定一个布尔标志，指示串行设备硬件是否反转的中断状态寄存器的内容。 如果**MaskInverted**均为非零，反转中断状态注册; 否则为中断状态注册不反转。 默认值**MaskInverted**为 0x00000000。

<a href="" id="serialskipexternalnaming--reg-dword-"></a>**SerialSkipExternalNaming** (REG\_DWORD)  
指定一个布尔标志，指示序列是否将为设备配置[COM 端口](configuration-of-com-ports.md)。 如果**SerialSkipExternalNaming**设置为 0x00000000，序列将设备配置为 COM 端口; 否则为序列不会配置设备作为 COM 端口。 默认值**SerialSkipExternalNaming**为 0x00000000。 有关序列如何将设备配置为 COM 端口的详细信息，请参阅[外部命名的 COM 端口](external-naming-of-com-ports.md)。

<a href="" id="serialrelinquishpowerpolicy--reg-dword-"></a>**SerialRelinquishPowerPolicy** (REG\_DWORD)  
指定指示序列是否为串行设备堆栈的电源策略所有者的布尔标志。 如果**SerialRelinquishPowerPolicy**为零，序列是电源策略所有者; 否则，序列不为电源策略所有者。 默认值**SerialRelinquishPowerPolicy**为 0x00000000。

<a href="" id="share-system-interrupt--reg-dword-"></a>**共享系统的中断**(REG\_DWORD)  
布尔型标志，用于指定是否允许系统以共享设备使用的中断。 如果**共享系统中断**为非零值，中断可以共享; 否则，不能共享中断。 默认值**共享系统中断**的值设置为**PermitShare**串行服务的条目值。 (默认服务值**PermitShare**为 0x00000000。)

<a href="" id="serialioresourcesindex--reg-dword-"></a>**SerialIoResourcesIndex** (REG\_DWORD)  
指定用于确定为设备设置的串行寄存器的 I/O 地址序列的部分资源描述符的索引。 默认值**SerialIoResourceIndex**为 0x00000000。

 

 




