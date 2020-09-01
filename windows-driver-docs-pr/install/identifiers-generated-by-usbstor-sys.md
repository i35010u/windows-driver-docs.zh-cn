---
title: USBSTOR.SYS 生成的标识符
description: USBSTOR.SYS 生成的标识符
ms.assetid: 5a5e1b68-9ec7-4a74-9b21-25f158a2a46c
keywords:
- USBSTOR.SYS WDK 设备安装
- 设备 Id WDK 设备安装
- USB 存储端口驱动程序 WDK 设备安装
- 存储端口驱动程序 WDK 设备安装
- 硬件 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c62a8ecede12fdcc35f19674bd33aeb772af3ba9
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097311"
---
# <a name="identifiers-generated-by-usbstorsys"></a>USBSTOR.SYS 生成的标识符





从 Windows 2000 开始，操作系统为许多 USB 大容量存储设备提供本机支持。 *Usbstor*安装文件包含明确支持的那些设备的设备 id。 如果 USB 集线器驱动程序枚举其中的一个设备，操作系统会自动加载 USB 存储端口驱动程序， *Usbstor.sys*。

*Usbstor*中的 usb 大容量存储设备的设备 id 采用常见的格式，适用于使用 usb 设备的设备描述符中的信息撰写的 Usb 设备 id：

USB \\ VID_v (4) # B0 PID_d (4) # B1 REV_r (4) 

其中：

-   * (4) * 是 USB 委员会分配给供应商的4位数供应商代码。

-   *d (4) * 是供应商分配给设备的4位数产品代码。

-   *r (4) * 是版本代码。

除这些设备 Id 外， *Usbstor* 还包含适用于类 8 ATAPI cd-rom 的兼容 id 以及支持批量传输的可移动媒体设备：

USB \\ CLASS_08&SUBCLASS_02&PROT_50

USB \\ CLASS_08&SUBCLASS_05&PROT_50

USB \\ CLASS_08&SUBCLASS_06&PROT_50

其中：

-   类 08h = 大容量存储设备。

-   子类 02h = SFF-8020i ATAPI CD-ROM 设备。

-   子类 05h = SFF-8070i ATAPI 可移动介质。

-   子类 06h = 通用 SCSI 媒体。

-   protocol 50h = 批量传输协议。

如果从设备的设备描述符检索到的数据与上述任何兼容 Id 都匹配，操作系统将加载 *Usbstor.sys*。

加载后，USB 存储端口驱动程序将为每个设备的逻辑单元创建新的 PDO。 有关详细信息，请参阅通过[USB 大容量存储设备的设备对象示例](../storage/device-object-example-for-a-usb-mass-storage-device.md)中所示*Usbstor.sys*创建的示例设备堆栈。

当 PnP 管理器查询新创建的 PDOs 的设备标识字符串时，USB 存储端口驱动程序会创建一组新的设备、硬件和兼容的 Id，该 Id 派生自设备的 SCSI 查询数据。 设备 ID 格式如下所示：

USBSTOR \\ (8) p (16) r (4) 

其中：

-   *v (8) * 是8个字符的供应商标识符。

-   *p (16) * 是16个字符的产品标识符。

-   *r (4) * 为4个字符的修订级别值。

磁盘驱动器的设备 ID 的示例如下所示：

USBSTOR \\ SEAGATE_ST39102LW_______0004

USB 存储端口驱动程序生成的硬件 Id 如下所示：

USBSTOR \\ t \* v (8) p (16) r (4) 

USBSTOR \\ t \* v (8) p (16) 

USBSTOR \\ t \* v (8) 

USBSTOR \\ (8) p (16) r (1) 

v (8) p (16) r (1) 

USBSTOR \\ GenericTypeString

GenericTypeString

其中：

- *t \* *是可变长度的 SCSI 设备类型代码。

- *v (8) * 是8个字符的供应商标识符。

- *p (16) * 是16个字符的产品标识符。

- *r (4) * 为4个字符的修订级别值。 在这些附加标识符中， *r (1) * 只表示修订标识符的第一个字符。

下表包含 USB 存储端口驱动程序用来生成标识符字符串的 SCSI 设备类型代码。

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
<td align="left"><p>DIRECT_ACCESS_DEVICE (0) </p></td>
<td align="left"><p>磁盘或 SFloppy</p></td>
<td align="left"><p>GenDisk 或 GenSFloppy</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEQUENTIAL_ACCESS_DEVICE (1) </p></td>
<td align="left"><p>顺序程序</p></td>
<td align="left"><p>GenSequential</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WRITE_ONCE_READ_MULTIPLE_DEVICE (4) </p></td>
<td align="left"><p>蠕虫</p></td>
<td align="left"><p>GenWorm</p></td>
</tr>
<tr class="even">
<td align="left"><p>READ_ONLY_DIRECT_ACCESS_DEVICE (5) </p></td>
<td align="left"><p>光盘</p></td>
<td align="left"><p>GenCdRom</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OPTICAL_DEVICE (7) </p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>GenOptical</p></td>
</tr>
<tr class="even">
<td align="left"><p>MEDIUM_CHANGER (8) </p></td>
<td align="left"><p>转换器</p></td>
<td align="left"><p>GenChanger</p></td>
</tr>
<tr class="odd">
<td align="left"><p>默认类型 (前面未列出的所有值) </p></td>
<td align="left"><p>其他</p></td>
<td align="left"><p>UsbstorOther</p></td>
</tr>
</tbody>
</table>

 

以下示例显示了 USB 存储端口驱动程序生成的硬件 Id：

USBSTOR \\ DiskSEAGATE_ST39102LW_______0004

USBSTOR \\ DiskSEAGATE_ST39102LW_______

USBSTOR \\ DiskSEAGATE_

USBSTOR \\ SEAGATE_ST39102LW_______0

SEAGATE_ST39102LW_______0

USBSTOR \\ GenDisk

GenDisk

USB 存储端口驱动程序会生成两个兼容的 Id。

USBSTOR \\ t\*

USBSTOR \\ RAW

其中*t \* *是可变长度的 SCSI 设备类型代码。

USB 存储端口驱动程序生成的兼容 Id 如下例所示：

USBSTOR \\ 磁盘

USBSTOR \\ RAW

 

