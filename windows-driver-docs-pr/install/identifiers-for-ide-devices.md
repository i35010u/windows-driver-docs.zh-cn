---
title: IDE 设备的标识符
description: IDE 设备的标识符
keywords:
- 设备标识字符串 WDK、IDE 设备
- 标识字符串 WDK 设备，IDE 设备
- 标识符 WDK 设备，IDE 设备
- IDE 设备标识符 WDK 设备安装
- 设备 Id WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
- 集成设备电子设备标识符 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e78a6754aa3ab9e90e8bbb2e4123b33a07b8c5b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826807"
---
# <a name="identifiers-for-ide-devices"></a>IDE 设备的标识符





集成设备电子设备的标识符 (IDE) 设备类似于 SCSI 标识符。 设备 ID 格式如下所示：

IDE \\ t \* v (40) r (8) 

其中：

- *t \** 是可变长度的设备类型的代码。

- *(40)* 是一个字符串，其中包含供应商名称、下划线、供应商的产品名称，以及用来将总到40个字符的下划线。

- *r (8)* 是8个字符的修订号。

除了设备 ID 之外，还有三个硬件 Id：

IDE \\ v (40) r (8) 

IDE \\ t \* v (40) 

 (40) r (8) 

与 SCSI 情况一样，只有一个兼容 ID，这种类型的泛型类型名称类似于 SCSI 端口驱动程序提供的标准 SCSI 类型名称，但只有11个条目，而不是十八个。 IDE 设备的一般设备类型名称如下：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IDE 类型代码</th>
<th align="left">设备类型</th>
<th align="left">泛型类型</th>
<th align="left">外围设备 ID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DIRECT_ACCESS_DEVICE (0) </p></td>
<td align="left"><p>磁盘</p></td>
<td align="left"><p>GenDisk</p></td>
<td align="left"><p>DiskPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEQUENTIAL_ACCESS_DEVICE (1) </p></td>
<td align="left"><p>顺序程序</p></td>
<td align="left"><p>GenSequential</p></td>
<td align="left"><p>TapePeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PRINTER_DEVICE (2) </p></td>
<td align="left"><p>打印机</p></td>
<td align="left"><p>GenPrinter</p></td>
<td align="left"><p>PrinterPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>PROCESSOR_DEVICE (3) </p></td>
<td align="left"><p>处理器</p></td>
<td align="left"><p>GenProcessor</p></td>
<td align="left"><p>OtherPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WRITE_ONCE_READ_MULTIPLE_DEVICE (4) </p></td>
<td align="left"><p>蠕虫</p></td>
<td align="left"><p>GenWorm</p></td>
<td align="left"><p>WormPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>READ_ONLY_DIRECT_ACCESS_DEVICE (5) </p></td>
<td align="left"><p>光盘</p></td>
<td align="left"><p>GenCdRom</p></td>
<td align="left"><p>CdRomPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCANNER_DEVICE (6) </p></td>
<td align="left"><p>扫描仪</p></td>
<td align="left"><p>GenScanner</p></td>
<td align="left"><p>ScannerPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>OPTICAL_DEVICE (7) </p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>GenOptical</p></td>
<td align="left"><p>OpticalDiskPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MEDIUM_CHANGER (8) </p></td>
<td align="left"><p>转换器</p></td>
<td align="left"><p>GenChanger</p></td>
<td align="left"><p>MediumChangerPeripheral</p></td>
</tr>
<tr class="even">
<td align="left"><p>COMMUNICATION_DEVICE (9) </p></td>
<td align="left"><p>Net</p></td>
<td align="left"><p>GenNet</p></td>
<td align="left"><p>CommunicationsPeripheral</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>其他</p></td>
<td align="left"><p>GenOther</p></td>
<td align="left"><p>OtherPeripheral</p></td>
</tr>
</tbody>
</table>

 

对于 IDE 转换器设备，一般类型名称是 **GenChanger** ，而不是 **ScsiChanger** ，对于通信设备，泛型类型名称为 **GenNet** ，而不是 **ScsiNet**。 对于顺序访问和 "处理器" 设备，SCSI 端口驱动程序将不返回任何通用名称，而 IDE 总线驱动程序将返回 **GenSequential** 和 **GenProcessor**。 此外，IDE 总线驱动程序只返回10个泛型类型，而 SCSI 端口驱动程序当前返回了十八。 在其他方面，由 IDE 总线驱动程序返回的一般名称与 SCSI 端口驱动程序返回的名称相同。

IDE 磁带驱动器的兼容 ID 如下：

GenSequential

在 LS-120 设备的特殊情况下，IDE 总线驱动程序将返回以下兼容 ID：

GenSFloppy

下面显示了可为 IDE 硬盘驱动器生成的标识符类型：

IDE \\ DiskMaxtor_91000D8_____________________SASX1B18

IDE \\ Maxtor_91000D8___________________________SASX1B18

IDE \\ DiskMaxtor_91000D8________________________

Maxtor_91000D8__________________________SASX1B18

GenDisk

 

 





