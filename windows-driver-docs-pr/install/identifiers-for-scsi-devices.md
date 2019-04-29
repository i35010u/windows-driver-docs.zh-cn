---
title: SCSI 设备的标识符
description: SCSI 设备的标识符
ms.assetid: 8bc68813-5096-40b2-bbd1-0aebb5a3326d
keywords:
- 设备标识字符串 WDK、 SCSI 设备
- SCSI 设备-设备标识字符串 WDK
- 标识符 WDK 设备，SCSI 设备
- SCSI 设备标识符 WDK 设备安装
- 设备 Id WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 917a542f60f67beb473cadc340232a481da0c3ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362995"
---
# <a name="identifiers-for-scsi-devices"></a>SCSI 设备的标识符





小型计算机系统接口 (SCSI) 设备的设备 ID 格式如下所示：

SCSI\\t\*v(8)p(16)r(4)

其中：

- *t\** 是可变长度的设备类型代码。

- *v(8)* 是 8 个字符供应商标识符。

- *p(16)* 是 16 个字符的产品标识符。

- *r(4)* 是 4 个字符的修订级别值。

总线枚举器确定通过内部字符串表，编制索引使用的数字编码的 SCSI 设备类型代码下, 表所示，通过查询设备，获取的设备类型。 其余的组件都是字符串返回设备，但带有特殊字符 （包括空格、 逗号、 和非打印的任何图形） 替换为下划线。

SCSI 端口驱动程序当前将返回以下设备类型字符串，其中的第九个对应于标准 SCSI 类型代码。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SCSI 类型代码</th>
<th align="left">设备类型</th>
<th align="left">泛型类型</th>
<th align="left">外围设备 ID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DIRECT_ACCESS_DEVICE (0)</p></td>
<td align="left"><p>Disk</p></td>
<td align="left"><p>GenDisk</p></td>
<td align="left"><p>DiskPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEQUENTIAL_ACCESS_DEVICE (1)</p></td>
<td align="left"><p>顺序</p></td>
<td align="left"></td>
<td align="left"><p>TapePeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PRINTER_DEVICE (2)</p></td>
<td align="left"><p>打印机</p></td>
<td align="left"><p>GenPrinter</p></td>
<td align="left"><p>PrinterPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>PROCESSOR_DEVICE (3)</p></td>
<td align="left"><p>处理器</p></td>
<td align="left"></td>
<td align="left"><p>OtherPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WRITE_ONCE_READ_MULTIPLE_DEVICE (4)</p></td>
<td align="left"><p>蠕虫</p></td>
<td align="left"><p>GenWorm</p></td>
<td align="left"><p>WormPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>READ_ONLY_DIRECT_ACCESS_DEVICE (5)</p></td>
<td align="left"><p>CdRom</p></td>
<td align="left"><p>GenCdRom</p></td>
<td align="left"><p>CdRomPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCANNER_DEVICE (6)</p></td>
<td align="left"><p>扫描仪</p></td>
<td align="left"><p>GenScanner</p></td>
<td align="left"><p>ScannerPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>OPTICAL_DEVICE (7)</p></td>
<td align="left"><p>光盘</p></td>
<td align="left"><p>GenOptical</p></td>
<td align="left"><p>OpticalDiskPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MEDIUM_CHANGER (8)</p></td>
<td align="left"><p>换带机</p></td>
<td align="left"><p>ScsiChanger</p></td>
<td align="left"><p>MediumChangerPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>COMMUNICATION_DEVICE (9)</p></td>
<td align="left"><p>Net</p></td>
<td align="left"><p>ScsiNet</p></td>
<td align="left"><p>CommunicationsPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>ASCIT8</p></td>
<td align="left"><p>ScsiASCIT8</p></td>
<td align="left"><p>ASCPrePressGraphicsPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>ASCIT8</p></td>
<td align="left"><p>ScsiASCIT8</p></td>
<td align="left"><p>ASCPrePressGraphicsPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>12</p></td>
<td align="left"><p>数组</p></td>
<td align="left"><p>ScsiArray</p></td>
<td align="left"><p>ArrayPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>13</p></td>
<td align="left"><p>机箱</p></td>
<td align="left"><p>ScsiEnclosure</p></td>
<td align="left"><p>EnclosurePeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>14</p></td>
<td align="left"><p>RBC</p></td>
<td align="left"><p>ScsiRBC</p></td>
<td align="left"><p>RBCPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>15</p></td>
<td align="left"><p>CardReader</p></td>
<td align="left"><p>ScsiCardReader</p></td>
<td align="left"><p>CardReaderPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>Bridge</p></td>
<td align="left"><p>ScsiBridge</p></td>
<td align="left"><p>BridgePeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>17</p></td>
<td align="left"><p>其他</p></td>
<td align="left"><p>ScsiOther</p></td>
<td align="left"><p>OtherPeripheral</p></td>
</tr>
</tbody>
</table>

 

磁盘驱动器的设备 ID 的示例将如下所示：

SCSI\\DiskSEAGATE_ST39102LW_______0004

有四个硬件 Id，除了设备 ID:

SCSI\\t\*v(8)p(16)

SCSI\\t\*v(8)

SCSI\\v(8)p(16)r(1)

V(8)p(16)r(1)

中的第三和第四个这些其他的标识符*r(1)* 表示只修订版本标识符的第一个字符。 以下示例说明了这些硬件 Id:

SCSI\\DiskSEAGATE_ST39102LW_______

SCSI\\DiskSEAGATE_

SCSI\\DiskSEAGATE_ST39102LW_______0

SEAGATE_ST39102LW_______0

SCSI 端口驱动程序提供了一个兼容 ID，从上表大小可变的泛型类型代码之一。

例如，磁盘驱动器的兼容 ID 如下所示：

GenDisk

因为 SCSI 驱动程序通常泛型 SCSI 设备超过任何其他的 INF 文件中使用通用标识符。 请注意，SCSI 端口驱动程序返回任何泛型名称在所有顺序访问权限和"处理器"的设备。

 

 





