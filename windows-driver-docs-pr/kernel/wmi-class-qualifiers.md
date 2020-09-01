---
title: WMI 类限定符
description: WMI 类限定符
ms.assetid: 62a00184-59b7-496d-b523-f4adb879d402
keywords:
- 类限定符 WDK WMI
- MOF 类限定符 WDK WMI
- embedded 类 WDK WMI
- 动态 MOF 限定符 WDK WMI
- 静态 MOF 限定符 WDK WMI
- 类 WDK WMI
- WMI WDK 内核，类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52c773410a51b51c7be65a06f1c6c3a576a941b5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190431"
---
# <a name="wmi-class-qualifiers"></a>WMI 类限定符





下表列出了必需的和可选的 MOF 类限定符，它们可用于描述驱动程序的 WMI 数据块和事件块。

*嵌入类*（作为另一个类中的数据项单独使用，不作为 WMI 数据块公开）只需要**WMI**和**Guid**限定符。 其他限定符与嵌入的类无关，将被忽略。 有关嵌入类的详细信息，请参阅 [驱动程序定义的 WMI 数据项](driver-defined-wmi-data-items.md)。

**动态** 和 **静态** 是标准 MOF 限定符。 有关其他标准 MOF 限定符的信息，请参阅 Microsoft Windows SDK。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>限定符</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Dynamic</strong></p></td>
<td><p>指示数据访问接口在运行时提供数据块的实例，而不是在 MOF 文件中提供静态数据的实例。 驱动程序向 WMI 注册的所有数据和事件块必须使用 <strong>动态</strong> 限定符定义。</p></td>
</tr>
<tr class="even">
<td><p><strong>Static</strong></p></td>
<td><p>指示数据访问接口在 MOF 文件中提供静态数据的实例，而不是在运行时提供数据块的实例。 由于静态数据驻留在 WMI 数据库中，驱动程序不会将静态数据块注册到 WMI。 MOF 文件中标记为 <strong>静态</strong> 的类不应由驱动程序的 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO&lt;/strong&gt;](./irp-mn-reginfo.md)"><strong>IRP_MN_REGINFO</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO_EX&lt;/strong&gt;](./irp-mn-reginfo-ex.md)"><strong>IRP_MN_REGINFO_EX</strong></a> 处理程序注册。</p></td>
</tr>
<tr class="odd">
<td><p><strong>提供程序 ( "WMIProv" ) </strong></p></td>
<td><p> (必需的) 指示类的提供程序是一个 WMI 提供程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>WMI</strong></p></td>
<td><p> (必需的) 指示类为 WMI 类。</p></td>
</tr>
<tr class="odd">
<td><p><strong>描述 ( "</strong><em>description-string</em><strong>" ) </strong></p></td>
<td><p> (可选) 指定 <strong>区域设置</strong> 限定符指定的区域设置的块说明。 如果已定义，WMI 客户端可以向用户显示说明字符串。 驱动程序编写器可以使用 <strong>说明</strong> 来记录类。</p></td>
</tr>
<tr class="even">
<td><p><strong>Guid ( "</strong><em>guid-string</em><strong>" ) </strong></p></td>
<td><p> (必需) 指定以字符串格式表示的 GUID，该 GUID 唯一地将块标识为 WMI。 驱动程序编写器应为驱动程序的 MOF 文件中的每个数据块生成 GUID，方法是使用 Windows SDK) 中包含的 guidgen.exe 或 uuidgen.exe (。 驱动程序注册其块时，驱动程序将 GUID 格式的此值传递给 WMI。 WMI 随后使用 GUID 在驱动程序的 MOF 资源中查找块的定义。</p></td>
</tr>
<tr class="odd">
<td><p><strong>区域设置 ( "MS &lt; /strong &gt; <em>locale-identifier</em><strong>" ) </strong></p></td>
<td><p> (可选) 指定由 <strong>Description</strong>指定的字符串的语言标识符和区域设置。 例如，0x804 的 <em>区域设置标识符</em> 指定美式英语。 单个 MOF 文件可以包含具有不同区域设置的块，但通常 MOF 文件中的所有块都具有相同的区域设置。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiExpense (</strong><em>支出-值</em><strong>) </strong></p></td>
<td><p> (可选) 指定收集数据块数据所需的平均 CPU 周期数。 例如，WMI 客户端可能会检查数据块的 <strong>WmiExpense</strong> 值，以确定查询其数据的频率。 如果省略 <strong>WmiExpense</strong> ，则假定 <em>支出-值</em> 为0。 <strong>WmiExpense</strong> 与注册数据块相比，收集成本高昂。</p></td>
</tr>
</tbody>
</table>

 

 

