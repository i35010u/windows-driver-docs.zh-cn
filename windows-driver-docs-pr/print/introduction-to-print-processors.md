---
title: 打印处理器介绍
description: 打印处理器介绍
ms.assetid: a34d8daa-b000-4501-8799-5f38cdf38ba4
keywords:
- 有关打印处理器的打印处理器 WDK，
- 自定义打印处理器 WDK
- 打印处理器 WDK，数据类型
- 数据类型 WDK 打印处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82e49973eabfd92f91ecffb3b564911b13d788b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527102"
---
# <a name="introduction-to-print-processors"></a>打印处理器介绍





打印处理器是负责将转换的打印作业的后台处理数据到可以发送到的格式的用户模式 Dll*的打印监视器*。 它们也要负责处理应用程序请求暂停、 恢复和取消打印作业。

打印作业的假脱机的数据包含在假脱机文件。 打印处理器读取的文件、 执行转换操作该数据流和将转换后的数据写入到后台处理程序。 后台处理程序然后将数据流发送到适当的打印监视器。

Microsoft Windows 2000 及更高版本包括下表中列出的打印处理器。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>打印处理器</th>
<th>输入的数据类型</th>
<th>输出数据类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Localspl.dll *</p></td>
<td><p>EMF</p>
<p>RAW</p>
<p>文本</p></td>
<td><p>RAW</p></td>
</tr>
<tr class="even">
<td><p>Sfmpsprt.dll</p></td>
<td><p>PSCRIPT1</p></td>
<td><p>RAW</p></td>
</tr>
</tbody>
</table>

 

\* 从 Windows 2000 开始，Localmon.dll 和 Winprint.dll 包含在 Localspl.dll。

有关数据类型的信息，请参阅以下主题：

[EMF 数据类型](emf-data-type.md)

[原始数据类型](raw-data-type.md)

[TEXT 数据类型](text-data-type.md)

[PSCRIPT1 数据类型](pscript1-data-type.md)

您可以创建自定义的打印处理器，以支持 Windows 2000 或更高版本的操作系统版本不支持的数据类型。 此外可以提供自定义的打印处理器支持一个或多个支持的数据类型，这样你就可以修改提供的打印处理器提供的功能。

打印处理器与相关联的打印机驱动程序在安装驱动程序，以便支持相同的数据类型的多个打印处理器可以共存。 有关详细信息，请参阅[安装打印处理器](installing-a-print-processor.md)。

**请注意**  打印处理器编译时，设置 Unicode 标志\#定义 UNICODE。 例如，打印处理器代码应使用类型为 LPWSTR，仅宽的字符串。

 

 

 




