---
title: 传统 COM 端口的注册表设置
description: 传统 COM 端口的注册表设置
ms.assetid: 043ac1f5-eeb1-4828-8417-b3c6d76b4322
keywords:
- 串行驱动程序 WDK、 COM 端口
- COM 端口 WDK 串行设备
- 串行设备 WDK、 COM 端口
- 传统的 COM 端口 WDK 串行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f74c82f59edc994e65027b175553c367e064af8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555721"
---
# <a name="registry-settings-for-a-legacy-com-port"></a>传统 COM 端口的注册表设置





本主题介绍序列使用包含旧的注册表设置[COM 端口](configuration-of-com-ports.md)。 序列始终将旧的串行设备配置为 COM 端口。

枚举旧的 COM 端口时，序列会查询这些条目的值。 如果不存在特定于设备的条目值，序列将使用串行服务值。

传统的 COM 端口的注册表设置不是下一个相应的旧版 COM 端口子项下 **...\\Services\\串行\\参数**密钥。

以下条目的值是与所述的相同[插串行设备](registry-settings-for-a-plug-and-play-serial-device.md):

-   **ClockRate**

-   **PortIndex**

-   **编制索引**

-   **RxFIFO**

-   **TxFIFO**

-   **MaskInverted**

-   **DisablePort**

-   **ForceFifoEnable**

与传统的 COM 端口使用以下其他项值：

<a href="" id="portaddress--reg-dword-"></a>**PortAddress** (REG\_DWORD)  
指定的 COM 端口控制寄存器中未转换的基本 I/O 地址。 序列中读取此值。 值不能为零。 默认值**PortAddress**为 0x00000000。

<a href="" id="interrupt--reg-dword-"></a>**中断**(REG\_DWORD)  
作为总线类型适用，指定未转换的中断向量。 序列中读取此值。 值不能为零。 默认值**中断**为 0x00000000。

<a href="" id="dosdevices--reg-sz-"></a>**DosDevices** (REG\_SZ)  
指定的 COM 端口的名称。 COM 端口的名称通常是 COM<em>&lt;n&gt;，</em>其中&lt; *n&gt;* 是从安装程序获取 COM 端口号[COM 端口数据库](com-port-database.md)。 但是，COM 端口名称可以设置为任何非**NULL**字符串。 序列使用的端口名称来创建在用户模式中可见的 COM 端口的符号链接。 默认值**DosDevices**是**NULL**字符串。

<a href="" id="interruptstatus--reg-dword-"></a>**InterruptStatus** (REG\_DWORD)  
指定的中断状态寄存器的原始 I/O 地址。 序列中读取此值。 如果端口是独立的端口，则省略值。 值不能为零，如果端口是多端口设备上。 默认值**InterruptStatus**为 0x00000000。

<a href="" id="busnumber--reg-dword-"></a>**BusNumber** (REG\_DWORD)  
指定总线类型的系统级总线的编号。 序列中读取此值。 默认值**BusNumber**为 0x00000000。

<a href="" id="bustype--reg-dword-"></a>**BusType** (REG\_DWORD)  
指定的总线类型。 序列中读取此值。 默认值**BusType**驱动程序初始化期间由序列。

<a href="" id="interruptmode--reg-dword-"></a>**InterruptMode** (REG\_DWORD)  
指定中断模式。 序列中读取此值。 默认值**InterruptMode**是 CM\_资源\_中断\_LATCHED。

<a href="" id="interruptlevel--reg-dword-"></a>**InterruptLevel** (REG\_DWORD)  
指定适合于总线类型的原始中断级别值。 序列中读取此值。 默认值**InterruptLevel**为 0x00000000。

<a href="" id="pnpdeviceid--reg-sz-"></a>**PnPDeviceID** (REG\_SZ)  
指定插设备的即插设备标识符。 序列中读取此值。 默认值**PnPDeviceID**是**NULL**字符串。

<a href="" id="legacydiscovered--reg-dword-"></a>**LegacyDiscovered** (REG\_DWORD)  
指示是否序列先前已向插管理器报告设备的布尔型标志。 串行读取和设置此值。 如果**LegacyDiscovered**为非零值，序列先前已报告设备并不会报告该设备。 否则为序列报告设备，并将项值设置为 0x00000001。

 

 




