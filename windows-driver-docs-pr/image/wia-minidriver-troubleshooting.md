---
title: 排查 WIA 微型驱动程序问题
description: 排查 WIA 微型驱动程序问题
ms.assetid: a0944bdd-56c4-4f7b-b542-eb353cd4d1f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a6057edfecf9868dfab28e0fdc6135d28a32474
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355194"
---
# <a name="wia-minidriver-troubleshooting"></a>排查 WIA 微型驱动程序问题





默认情况下，WIA 服务将记录错误到名为的文件*wiadebug.log*中 **%** <em>windir</em> **%** 目录。 WIA 服务放入此文件中的信息可以在驱动程序开发过程是很有帮助。 下面的示例描述了典型的问题，并演示如何在中的信息*wiadebug.log*文件可用于查找问题的解决方案。

开发人员编写的应用程序来测试正在开发的扫描程序驱动程序。 作为测试之一，开发人员尝试设置的扫描程序以每英寸点数 (dpi) 为 1200，但此操作会生成错误的通知。 查看 Wiadebug.log 文件显示如下信息：

```console
wiasGetChangedValueLong, validate prop 6147 failed hr: 0x80070057
wiasUpdateScanRect, CheckXResAndUpdate failed (0x80070057)
CDrvWrap::WIA_drvValidateItemProperties, Error calling driver:
drvValidateItemProperties with hr = 0x80070057 (This is normal if the app wrote an invalid value)
```

这些日志条目指示驱动程序正在报告应用程序编写了一个无效值。 将无法根据此信息确定确切的问题是什么。 如果开发人员增加到报告警告和错误的 WIA 日志记录级别*wiadebug.log*生成类似于以下输出：

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

该输出显示水平分辨率属性导致了故障。 应用程序尝试将分辨率设置为 1200，但支持的分辨率列表不包括 1200年。 因此，WIA 服务验证帮助程序[ **wiasValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasvalidateitemproperties)拒绝该请求将此值设置。

现在，识别了问题，它是由开发人员确定它是否是驱动程序，或者必须修改该应用程序。 如果扫描程序的规范允许其支持 100 到 1400 dpi 之间的所有解决方法，该驱动程序应能处理对 1200 dpi 的请求。 如果扫描程序不支持此设置，应更改应用程序，因此它不会尝试将水平分辨率设置为不能用于此属性的值。 在这种情况下，应用程序应然后检查一个值，然后再尝试将属性设置为此值有效。

在注册表中的条目由控制日志记录级别。 对于 WIA，此密钥驻留在：

**HKLM\\System\\CurrentControlSet\\Control\\StillImage\\Debug\\** <em>MODULE\_NAME</em> **\\DebugFlags**

在此示例中，模块\_名称是相应的二进制模块的名称。 对于 WIA 服务，这是*wiaservc.dll*。 中的值**设调试标志**控制日志记录级别。 下表中指定了三种设置：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
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

中的值**设调试标志**是标志值 （即，不同的设置可能与结合使用按位 OR 运算符）。 若要启用日志记录错误、 警告和跟踪一次，将设置**设调试标志**0x0000007 到。

按顺序的值的变化**设调试标志**才会生效，WIA 服务 (*stisvc*) 必须停止并重新启动。 请参阅[启动和停止静止图像服务](starting-and-stopping-the-still-image-service.md)有关详细信息。

**请注意**  过多的日志记录可能会导致性能显著降低。 仅当尝试解决特定问题时，应增加日志记录级别。 问题解决后，设置到其原始级别日志记录。 默认日志记录级别是一个。 请勿增加三个以上的日志记录级别，因为这可能会导致崩溃。
