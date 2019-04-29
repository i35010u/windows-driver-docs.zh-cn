---
title: WMI 类限定符
description: WMI 类限定符
ms.assetid: 62a00184-59b7-496d-b523-f4adb879d402
keywords:
- 类限定符 WDK WMI
- MOF 类限定符 WDK WMI
- 嵌入的 WDK WMI 类
- 动态 MOF 限定符 WDK WMI
- 静态 MOF 限定符 WDK WMI
- WDK WMI 类
- WMI WDK 内核类
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ebbe1965c85dee13af57a4e2817ae7930df8845
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393014"
---
# <a name="wmi-class-qualifiers"></a>WMI 类限定符





下表列出的必需和可选 MOF 类限定符可以用于描述驱动程序的 WMI 数据块和事件块。

*嵌入类*，它是一个类仅用作另一个类中的数据项，并且不公开为 WMI 数据块，仅要求**WMI**并**Guid**限定符。 其他限定符不相关的嵌入的类，并将被忽略。 有关嵌入类的详细信息，请参阅[驱动程序定义的 WMI 数据项目](driver-defined-wmi-data-items.md)。

**动态**并**静态**是标准 MOF 限定符。 有关其他标准 MOF 限定符的信息，请参阅 Microsoft Windows SDK。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>限定符</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Dynamic</strong></p></td>
<td><p>指示数据提供程序在运行的时，而不提供在 MOF 文件中的静态数据的实例提供数据块的实例。 必须使用定义向 WMI 注册驱动程序的所有数据和事件块<strong>动态</strong>限定符。</p></td>
</tr>
<tr class="even">
<td><p><strong>Static</strong></p></td>
<td><p>指示数据提供程序提供了在 MOF 文件中，而不是在运行时提供的数据块的实例的静态数据的实例。 驱动程序不使用 WMI，注册静态数据块，因为静态数据驻留在 WMI 数据库。 类标记为<strong>静态</strong>在 MOF 文件不应注册由驱动程序的<a href="https://msdn.microsoft.com/library/windows/hardware/ff551731" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551731)"> <strong>IRP_MN_REGINFO</strong> </a>或者<a href="https://msdn.microsoft.com/library/windows/hardware/ff551734" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO_EX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551734)"> <strong>IRP_MN_REGINFO_EX</strong> </a>处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Provider("WMIProv")</strong></p></td>
<td><p>（必需）指示提供程序类的 WMI 提供程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>WMI</strong></p></td>
<td><p>（必需）指示该类是一个 WMI 类。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Description("</strong><em>description-string</em><strong>")</strong></p></td>
<td><p>（可选）指定用于通过指定的区域设置的块的说明<strong>区域设置</strong>限定符。 如果定义，WMI 客户端可以向用户显示的描述字符串。 驱动程序编写器可以使用<strong>说明</strong>记录类。</p></td>
</tr>
<tr class="even">
<td><p><strong>Guid("</strong><em>guid-string</em><strong>")</strong></p></td>
<td><p>（必需）指定 GUID 字符串格式，用于唯一标识与 WMI 的块。 驱动程序编写器应生成每个数据块的 GUID 在驱动程序的 MOF 文件中，使用 guidgen.exe 或 uuidgen.exe （这包括在 Windows SDK 中）。 当驱动程序注册其块时，驱动程序将此值采用 GUID 格式传递到 WMI。 然后，WMI 使用 GUID 来查找驱动程序的 MOF 资源中的块的定义。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Locale("MS&lt;/strong&gt;<em>locale-identifier</em><strong>")</strong></p></td>
<td><p>（可选）指定的语言标识符和指定的字符串的区域设置<strong>说明</strong>。 例如，<em>区域设置标识符</em>的 0x409 指定美国英语。 单个的 MOF 文件可以包含不同的区域设置的块，但通常所有 MOF 文件中的块具有相同的区域设置。</p></td>
</tr>
<tr class="even">
<td><p><strong>WmiExpense(</strong><em>expense-value</em><strong>)</strong></p></td>
<td><p>（可选）指定收集的数据块数据所需的 CPU 周期的平均数。 例如，WMI 客户端检查的数据块<strong>WmiExpense</strong>值，以确定经常查询其数据的方式。 如果<strong>WmiExpense</strong>省略，则<em>费用值</em>被假定为 0。 <strong>WmiExpense</strong>无关注册为成本高昂，若要收集的数据块。</p></td>
</tr>
</tbody>
</table>

 

 

 




