---
title: USBSTOR.SYS 生成的标识符
description: USBSTOR.SYS 生成的标识符
ms.assetid: 5a5e1b68-9ec7-4a74-9b21-25f158a2a46c
keywords:
- USBSTOR。SYS WDK 设备安装
- 设备 Id WDK 设备安装
- USB 存储端口驱动程序 WDK 设备安装
- 存储端口驱动程序 WDK 设备安装
- 硬件 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50bed89d8b75bd90087c5a4a129570bed30ea29f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327815"
---
# <a name="identifiers-generated-by-usbstorsys"></a>USBSTOR.SYS 生成的标识符





操作系统从 Windows 2000 开始，对于很多 USB 大容量存储设备提供本机支持。 *Usbstor.inf*安装文件包含显式支持这些设备的设备 Id。 如果 USB 集线器驱动程序枚举这些设备之一，操作系统会自动加载 USB 存储端口驱动程序， *Usbstor.sys*。

USB 设备 Id 大容量存储设备中的*Usbstor.inf*使用 USB 设备的设备描述符中的信息来撰写的 USB 设备 id 采用以下常规形式：

USB\\VID_v(4)&PID_d(4)&REV_r(4)

其中：

-   *v(4)* 是 USB 委员会将分配给供应商的 4 位供应商代码。

-   *d(4)* 是供应商将分配给设备的 4 个数字的产品代码。

-   *r(4)* 是修订代码。

下列设备 Id，除了*Usbstor.inf*类 8 ATAPI CD-ROM 和可移动介质设备的支持仅限大容量的传输包含兼容 Id:

USB\\CLASS_08&SUBCLASS_02&PROT_50

USB\\CLASS_08&SUBCLASS_05&PROT_50

USB\\CLASS_08&SUBCLASS_06&PROT_50

其中：

-   类 08 h = 大容量存储设备。

-   子类 02 h = SFF 8020i ATAPI CD-ROM 设备。

-   子类 05 h = SFF 8070i ATAPI 可移动介质。

-   子类 06 h = 泛型 SCSI 媒体。

-   协议 50 h = 仅限大容量的传输协议。

如果从设备的设备描述符检索的数据与任何这些兼容 Id 匹配，将加载操作系统*Usbstor.sys*。

只要将加载它，USB 存储端口驱动程序会为每个设备的逻辑单元创建一个新的 PDO。 有关详细信息，请参阅创建的示例设备堆栈*Usbstor.sys*中所示[USB 大容量存储设备的设备对象示例](https://msdn.microsoft.com/windows/hardware/drivers/storage/device-object-example-for-a-usb-mass-storage-device)。

当新创建的 PDOs 的设备标识字符串的即插即用管理器查询，USB 存储端口驱动程序创建一组新的设备时，硬件和兼容 Id 将派生自设备的 SCSI 查询数据。 设备 ID 格式如下所示：

USBSTOR\\v(8)p(16)r(4)

其中：

-   *v(8)* 是 8 个字符供应商标识符。

-   *p(16)* 是 16 个字符的产品标识符。

-   *r(4)* 是 4 个字符的修订级别值。

磁盘驱动器的设备 ID 的示例将如下所示：

USBSTOR\\SEAGATE_ST39102LW_______0004

硬件 Id 的 USB 存储端口驱动程序将生成如下所示：

USBSTOR\\t\*v(8)p(16)r(4)

USBSTOR\\t\*v(8)p(16)

USBSTOR\\t\*v(8)

USBSTOR\\v(8)p(16)r(1)

v(8)p(16)r(1)

USBSTOR\\GenericTypeString

GenericTypeString

其中：

- *t\** 是可变长度的 SCSI 设备类型代码。

- *v(8)* 是 8 个字符供应商标识符。

- *p(16)* 是 16 个字符的产品标识符。

- *r(4)* 是 4 个字符的修订级别值。 在这些其他的标识符*r(1)* 表示只修订版本标识符的第一个字符。

下表包含 USB 存储端口驱动程序用来生成标识符的字符串的 SCSI 设备类型代码。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SCSI 类型代码</th>
<th align="left">设备类型</th>
<th align="left">泛型类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DIRECT_ACCESS_DEVICE (0)</p></td>
<td align="left"><p>磁盘或 SFloppy</p></td>
<td align="left"><p>GenDisk 或 GenSFloppy</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEQUENTIAL_ACCESS_DEVICE (1)</p></td>
<td align="left"><p>顺序</p></td>
<td align="left"><p>GenSequential</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WRITE_ONCE_READ_MULTIPLE_DEVICE (4)</p></td>
<td align="left"><p>蠕虫</p></td>
<td align="left"><p>GenWorm</p></td>
</tr>
<tr class="even">
<td align="left"><p>READ_ONLY_DIRECT_ACCESS_DEVICE (5)</p></td>
<td align="left"><p>CdRom</p></td>
<td align="left"><p>GenCdRom</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OPTICAL_DEVICE (7)</p></td>
<td align="left"><p>光盘</p></td>
<td align="left"><p>GenOptical</p></td>
</tr>
<tr class="even">
<td align="left"><p>MEDIUM_CHANGER (8)</p></td>
<td align="left"><p>换带机</p></td>
<td align="left"><p>GenChanger</p></td>
</tr>
<tr class="odd">
<td align="left"><p>默认类型 （未列出以前的所有值）</p></td>
<td align="left"><p>其他</p></td>
<td align="left"><p>UsbstorOther</p></td>
</tr>
</tbody>
</table>

 

这些示例中显示的硬件 Id 生成的 USB 存储端口驱动程序：

USBSTOR\\DiskSEAGATE_ST39102LW_______0004

USBSTOR\\DiskSEAGATE_ST39102LW_______

USBSTOR\\DiskSEAGATE_

USBSTOR\\SEAGATE_ST39102LW_______0

SEAGATE_ST39102LW_______0

USBSTOR\\GenDisk

GenDisk

USB 存储端口驱动程序将生成两个兼容 Id。

USBSTOR\\t\*

USBSTOR\\RAW

其中*t\** 是可变长度的 SCSI 设备类型代码。

以下示例阐释了生成的 USB 存储端口驱动程序的兼容 Id:

USBSTOR\\磁盘

USBSTOR\\RAW

 

 





