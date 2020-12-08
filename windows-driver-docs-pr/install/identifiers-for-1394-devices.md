---
title: 1394 设备的标识符
description: 1394 设备的标识符
keywords:
- 设备标识字符串 WDK，1394设备
- 标识字符串 WDK 设备，1394设备
- 标识符 WDK 设备，1394设备
- 1394设备标识符 WDK 设备安装
- 设备 Id WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b56dd9ee3b7f40dbfaa9ceaaec154344179dc81d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828623"
---
# <a name="identifiers-for-1394-devices"></a>1394 设备的标识符





1394总线驱动程序为设备构造这些标识符：

1394 \\ VendorName&ModelName

1394 \\ UnitSpecId&UnitSwVersion

其中：

-   *VendorName* 是硬件供应商的名称。

-   *ModelName* 标识设备。

-   *UnitSpecId* 标识软件规范机构。

-   *UnitSwVersion* 标识软件规格。

用于构造这些标识符的信息来自设备的配置 ROM。

如果设备具有供应商和型号名称字符串，1394总线驱动程序会使用第一个标识符，即设备 ID 和硬件 ID，第二个标识符用作兼容 ID。 如果设备缺少供应商或型号名称字符串，则总线驱动程序会使用第二个标识符，即设备 ID 和兼容的 ID，并在查询硬件 ID 时返回双精度 null。 因此，在某些情况下，IEEE1394 总线驱动程序提供了设备 ID，但没有硬件 ID。 这是常规规则的例外，设备 ID 是硬件 Id 之一。

IEEE1394 上相机的设备 ID 可能是：

1394 \\ 索尼&CCM-DS250_1

对于设备的配置 ROM 中的每个单元目录，多功能设备都有单独的标识符集。

如果设备的函数驱动程序位于 SBP-2 端口驱动程序的顶层，则其设备 ID 采用以下格式。

SBP2 \\ VendorName&ModelName&LUNn\*

其中：

-   *VendorName* 是硬件供应商。

-   *ModelName* 标识设备。

-   *n* \* 是一个字符串，表示以十六进制表示的逻辑单元号的低序位2个字节。 多功能设备上的各种功能生成的设备 Id 与此数字除外。

2 1394 SBP 硬盘的设备 ID 可能如下所示：

SBP2 \\ VST_TECHNOLOGIESINC &VST_FULL_HEIGHT_FIREWIRE_DRIVE&LUN0

与1394总线一样，SBP2 端口驱动程序不会将设备 ID 分类为硬件 ID。 但是，1394总线区分硬件 Id 和兼容 Id，而 SBP2 端口驱动程序则不会。 对于 **BusQueryHardwareIDs** 类型的 **IRP_MN_QUERY_ID** irp 和 **BusQueryCompatibleIDs** SBP2 类型的 **IRP_MN_QUERY_ID** irp，返回一组四个标识符：

SBP2 \\ VendorName&ModelName&CmdSetIdn\*

SBP2 \\ Gen

常规

SBP2 \\ n \*&d\*

其中：

- *n \** 为命令集 ID 号。

- *Gen* 是在下表的 "泛型类型" 列中列出的通用名称之一。

- *d \** 是通过使用逻辑单元号的前两个字节中的较低五位构成的数字。 此数字是对应于 *Gen* 字符串标识符的设备的通用名称的数值代码。

上一个示例中列出的第四个 ID (SBP2 \\ *n \*&\* d*) ，它在所有 SBP2 硬件标识符中是唯一的，其中，硬件标识符中的每个都是 *n \**，命令集 ID 号和 *d \**，一般名称的数字代码为十进制，而不是十六进制。

此表列出了 SBP2 端口驱动程序返回的通用设备名称。 SBP2 端口驱动程序生成的大多数（但不是全部）通用名称是 SCSI 端口驱动程序生成的一个子集。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">1394类型代码</th>
<th align="left">设备类型</th>
<th align="left">泛型类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>RBC_DEVICE 或 DIRECT_ACCESS_DEVICE (0) </p></td>
<td align="left"><p>磁盘</p></td>
<td align="left"><p>GenDisk</p></td>
</tr>
<tr class="even">
<td align="left"><p>SEQUENTIAL_ACCESS_DEVICE (1) </p></td>
<td align="left"><p>顺序程序</p></td>
<td align="left"><p>GenSequential</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PRINTER_DEVICE (2) </p></td>
<td align="left"><p>打印机</p></td>
<td align="left"><p>GenPrinter</p></td>
</tr>
<tr class="even">
<td align="left"><p>WRITE_ONCE_READ_MULTIPLE_DEVICE (4) </p></td>
<td align="left"><p>蠕虫</p></td>
<td align="left"><p>GenWorm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>READ_ONLY_DIRECT_ACCESS_DEVICE (5) </p></td>
<td align="left"><p>光盘</p></td>
<td align="left"><p>GenCdRom</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCANNER_DEVICE (6) </p></td>
<td align="left"><p>扫描仪</p></td>
<td align="left"><p>GenScanner</p></td>
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
<td align="left"><p>默认类型 (以上列出的所有值) </p></td>
<td align="left"><p>其他</p></td>
<td align="left"><p>GenSbp2Device</p></td>
</tr>
</tbody>
</table>

 

 

 





