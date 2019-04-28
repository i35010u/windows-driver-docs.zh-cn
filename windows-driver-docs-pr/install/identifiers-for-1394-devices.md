---
title: 1394 设备的标识符
description: 1394 设备的标识符
ms.assetid: 6ab2538a-af4c-4c46-bda5-abb431c5bd6b
keywords:
- 设备标识字符串 WDK，1394年设备
- 1394 设备-设备标识字符串 WDK
- 标识符 WDK 设备，1394年设备
- 1394 设备标识符 WDK 设备安装
- 设备 Id WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80c1ce1e6a3f9261b6619f483b47fdee6a80f43c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335350"
---
# <a name="identifiers-for-1394-devices"></a>1394 设备的标识符





1394 总线驱动程序构造这些标识符的设备：

1394\\VendorName&ModelName

1394\\UnitSpecId&UnitSwVersion

其中：

-   *VendorName*硬件供应商的名称。

-   *ModelName*标识的设备。

-   *UnitSpecId*标识软件规范颁发机构。

-   *UnitSwVersion*标识软件规范。

用于构造这些标识符的信息来自设备的配置 rom。

1394 总线驱动程序作为兼容 id。 如果设备具有供应商和模型名称字符串，使用作为设备 ID 和硬件 ID，第一个标识符和第二个标识符 如果设备缺少供应商或模型名称字符串，总线驱动程序作为设备 ID 和兼容 ID，使用第二个标识符，并返回双 null，如果查询的硬件 id。 因此，IEEE1394 总线驱动程序，在某些情况下，提供设备 ID，但没有硬件 id。 这是一般的规则的设备 ID 是一个硬件 Id 的例外。

IEEE1394 上的摄像头的设备 ID 可能是：

1394\\SONY&CCM-DS250_1.08

多功能设备具有单独的一组标识符对于每个单元目录中设备的配置 rom。

如果设备的功能驱动程序位于 sbp-2 端口驱动程序之上，其设备 ID 会采用以下格式。

SBP2\\VendorName&ModelName&LUNn\*

其中：

-   *VendorName*是硬件供应商。

-   *ModelName*标识的设备。

-   *n* \*是一个字符串，表示以十六进制格式的逻辑单元号较低序位 2 个字节。 各种功能的多功能设备上生成设备 Id 的相同，仅此数字。

Sbp-2 1394 硬盘的设备 ID 可能按如下所示：

SBP2\\VST_TECHNOLOGIESINC.&VST_FULL_HEIGHT_FIREWIRE_DRIVE&LUN0

作为用于 1394年总线 SBP2 端口驱动程序不会不进行分类的设备 ID 作为硬件 id。 但是，而硬件 Id 和兼容 Id 之间是有区别的 1394年总线，SBP2 端口驱动程序将不执行。 有关**IRP_MN_QUERY_ID** Irp 类型**BusQueryHardwareIDs**并**IRP_MN_QUERY_ID**类型的 Irp **BusQueryCompatibleIDs** SBP2返回一组相同的四个标识符：

SBP2\\VendorName&ModelName&CmdSetIdn\*

SBP2\\常规

常规

SBP2\\n\*&d\*

其中：

- *n\** 命令设置 ID 号。

- *常规*是一个泛型类型列的下表中列出的一般名称。

- *d\** 数字格式是采用较低的逻辑单元号上两个字节的五位。 此数字是对应于设备的通用名称的数值代码*常规*字符串标识符。

上一示例中列出的第四个 ID (SBP2\\*n\*（& d)\**)，在中，所有 SBP2 硬件标识符是唯一的同时*n\** ，命令设置 ID 号和*d\**，通用名称的数值代码以十进制，不是十六进制。

此表列出了返回 SBP2 端口驱动程序的通用设备名称。 最多，而不是全部 SBP2 端口驱动程序生成的通用名称是由 SCSI 端口驱动程序的子集。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">1394 类型代码</th>
<th align="left">设备类型</th>
<th align="left">泛型类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>RBC_DEVICE 或 DIRECT_ACCESS_DEVICE (0)</p></td>
<td align="left"><p>Disk</p></td>
<td align="left"><p>GenDisk</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEQUENTIAL_ACCESS_DEVICE (1)</p></td>
<td align="left"><p>顺序</p></td>
<td align="left"><p>GenSequential</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PRINTER_DEVICE (2)</p></td>
<td align="left"><p>打印机</p></td>
<td align="left"><p>GenPrinter</p></td>
</tr>
<tr class="even">
<td align="left"><p>WRITE_ONCE_READ_MULTIPLE_DEVICE (4)</p></td>
<td align="left"><p>蠕虫</p></td>
<td align="left"><p>GenWorm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>READ_ONLY_DIRECT_ACCESS_DEVICE (5)</p></td>
<td align="left"><p>CdRom</p></td>
<td align="left"><p>GenCdRom</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCANNER_DEVICE (6)</p></td>
<td align="left"><p>扫描仪</p></td>
<td align="left"><p>GenScanner</p></td>
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
<td align="left"><p>默认类型 （上面未列出的所有值）</p></td>
<td align="left"><p>其他</p></td>
<td align="left"><p>GenSbp2Device</p></td>
</tr>
</tbody>
</table>

 

 

 





