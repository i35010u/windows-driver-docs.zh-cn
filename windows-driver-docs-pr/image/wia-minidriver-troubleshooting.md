---
title: 排查 WIA 微型驱动程序问题
description: 排查 WIA 微型驱动程序问题
ms.assetid: a0944bdd-56c4-4f7b-b542-eb353cd4d1f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37be79dce324cd0c7ce96f54c2eec0b9c766763c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840675"
---
# <a name="wia-minidriver-troubleshooting"></a>排查 WIA 微型驱动程序问题





默认情况下，WIA 服务将错误记录到 **%** <em>windir</em> **%** 目录下名为*wiadebug*的文件中。 WIA 服务放置在此文件中的信息在驱动程序开发过程中非常有用。 下面的示例描述了一个典型的问题，并演示了如何使用*wiadebug*文件中的信息来查找该问题的解决方案。

开发人员编写一个应用程序来测试正在开发的扫描仪驱动程序。 作为测试之一，开发人员尝试将扫描仪的每英寸点数（dpi）设置为1200，但通知此操作将产生错误。 Wiadebug 文件的外观如下所示：

```console
wiasGetChangedValueLong, validate prop 6147 failed hr: 0x80070057
wiasUpdateScanRect, CheckXResAndUpdate failed (0x80070057)
CDrvWrap::WIA_drvValidateItemProperties, Error calling driver:
drvValidateItemProperties with hr = 0x80070057 (This is normal if the app wrote an invalid value)
```

这些日志条目指示驱动程序报告应用程序写入的值无效。 对于此信息并不清楚，确切的问题是什么。 如果开发人员增加了 WIA 日志记录级别以报告警告以及错误， *wiadebug*会生成类似于以下内容的输出：

```console
wiasValidateItemProperties, invalid LIST value for : 
    (propID) Horizontal Resolution, value = 1200
Valid values are:
    75
    100
    150
    200
    300
    600
 wiasGetChangedValueLong, validate prop 6147 failed hr: 0x80070057
wiasUpdateScanRect, CheckXResAndUpdate failed (0x80070057)
 CDrvWrap::WIA_drvValidateItemProperties, Error calling driver: 
 drvValidateItemProperties with hr = 0x80070057 (This is normal if the app wrote an invalid value)
```

输出显示水平解析属性导致失败。 应用程序尝试将分辨率设置为1200，但支持的解决方法列表中不包括1200。 因此，WIA 服务验证帮助器[**wiasValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasvalidateitemproperties)拒绝设置此值的请求。

确定问题后，开发人员需要确定是否为驱动程序或必须修改的应用程序。 如果扫描仪的规格允许它支持100和 1400 dpi 之间的所有分辨率，则驱动程序应能够处理 1200 dpi 的请求。 如果扫描程序不支持此设置，则应更改应用程序，使其不会尝试将水平分辨率设置为对此属性无效的值。 在这种情况下，应用程序应检查值是否有效，然后再尝试将属性设置为此值。

日志记录级别由注册表中的条目控制。 对于 WIA，此密钥位于：

**HKLM\\System\\CurrentControlSet\\控件\\StillImage\\调试\\** <em>模块\_名称</em> **\\DebugFlags**

在此示例中，MODULE\_名称是相应的二进制模块的名称。 对于 WIA 服务，此为*wiaservc*。 **DebugFlags**中的值控制日志记录级别。 下表中提供了三种设置：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00000001</p></td>
<td><p>显示错误消息。</p></td>
</tr>
<tr class="even">
<td><p>0x00000002</p></td>
<td><p>显示警告消息。</p></td>
</tr>
<tr class="odd">
<td><p>0x00000004</p></td>
<td><p>显示跟踪消息。</p></td>
</tr>
</tbody>
</table>

**DebugFlags**中的值是一个标志值（即，可以与按位 or 运算符组合的设置不同）。 若要同时启用记录错误、警告和跟踪，请将**DebugFlags**设置为0x0000007。

为了使**DebugFlags**的值更改生效，必须停止 WIA 服务（*stisvc*），然后重新启动。 有关详细信息，请参阅[启动和停止静止映像服务](starting-and-stopping-the-still-image-service.md)。

**请注意**   过多的日志记录可能会导致性能显著降低。 仅当尝试解决特定问题时，才应增加日志记录级别。 更正问题后，将日志记录设置为其原始级别。 默认日志记录级别为1。 不要将日志记录级别增加三个，因为这可能会导致崩溃。
