---
title: 用于旧版 COM 端口的注册表设置
description: 用于旧版 COM 端口的注册表设置
keywords:
- 串行驱动程序 WDK，COM 端口
- COM 端口 WDK 串行设备
- 串行设备 WDK，COM 端口
- 旧 COM 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b1ddc46ad4c23d2572a2e4f1875ba9c08277d50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804999"
---
# <a name="registry-settings-for-a-legacy-com-port"></a>用于旧版 COM 端口的注册表设置





本主题介绍串行用于旧 [COM 端口](configuration-of-com-ports.md)的注册表设置。 串行始终将旧版串行设备配置为 COM 端口。

在枚举旧 COM 端口时，串行查询这些输入值。 如果设备特定的条目值不存在，则串行使用串行服务值。

旧 COM 端口的注册表设置位于 "" 下的相应旧版 COM 端口子项下 **。 \\Services \\ 串行 \\ 参数** 密钥。

以下条目值与 [即插即用串行设备](registry-settings-for-a-plug-and-play-serial-device.md)的描述相同：

-   **ClockRate**

-   **PortIndex**

-   **作**

-   **RxFIFO**

-   **TxFIFO**

-   **MaskInverted**

-   **DisablePort**

-   **ForceFifoEnable**

以下附加条目值与旧式 COM 端口一起使用：

<a href="" id="portaddress--reg-dword-"></a>**PortAddress** (REG \_ DWORD)   
指定 COM 端口控制寄存器的未转换的基本 i/o 地址。 串行读取此值。 该值不能为零。 **PortAddress** 的默认值为0x00000000。

<a href="" id="interrupt--reg-dword-"></a>**中断** (REG \_ DWORD)   
根据相应的总线类型指定未翻译的中断向量。 串行读取此值。 该值不能为零。 **中断** 的默认值为0x00000000。

<a href="" id="dosdevices--reg-sz-"></a>**DosDevices** (REG \_ SZ)   
指定 COM 端口的名称。 COM 端口的名称通常是 COM <em> &lt; n &gt; ，</em>其中 &lt; *n &gt;* 是安装程序从 [com 端口数据库](com-port-database.md)获得的 com 端口号。 但是，COM 端口名称可以设置为任何非 **空** 字符串。 串行使用端口名称创建指向 COM 端口（在 usermode 中可见）的符号链接。 **DosDevices** 的默认值为 **空** 字符串。

<a href="" id="interruptstatus--reg-dword-"></a>**InterruptStatus** (REG \_ DWORD)   
指定中断状态寄存器的原始 i/o 地址。 串行读取此值。 如果端口是独立端口，则忽略该值。 如果端口位于多端口设备上，则该值不能为零。 **InterruptStatus** 的默认值为0x00000000。

<a href="" id="busnumber--reg-dword-"></a>**BusNumber** (REG \_ DWORD)   
指定总线类型的系统范围总线号。 串行读取此值。 **BusNumber** 的默认值为0x00000000。

<a href="" id="bustype--reg-dword-"></a>**BusType** (REG \_ DWORD)   
指定总线类型。 串行读取此值。 **BusType** 的默认值是在驱动程序初始化期间由串行确定的。

<a href="" id="interruptmode--reg-dword-"></a>**InterruptMode** (REG \_ DWORD)   
指定中断模式。 串行读取此值。 **InterruptMode** 的默认值为 CM \_ 资源 \_ 中断 \_ 锁定。

<a href="" id="interruptlevel--reg-dword-"></a>**InterruptLevel** (REG \_ DWORD)   
指定适用于总线类型的原始中断级别值。 串行读取此值。 **InterruptLevel** 的默认值为0x00000000。

<a href="" id="pnpdeviceid--reg-sz-"></a>**PnPDeviceID** (REG \_ SZ)   
为即插即用设备指定即插即用设备标识符。 串行读取此值。 **PnPDeviceID** 的默认值为 **空** 字符串。

<a href="" id="legacydiscovered--reg-dword-"></a>**LegacyDiscovered** (REG \_ DWORD)   
布尔型标志，指示串行是否先前已将设备报告给即插即用管理器。 串行读取并设置此值。 如果 **LegacyDiscovered** 为非零，则串行先前报告了设备，并且不会再次报告设备。 否则，Serial 会报告设备，并将输入值设置为0x00000001。

 

 




