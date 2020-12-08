---
title: 打印处理器简介
description: 打印处理器简介
keywords:
- 打印处理器 WDK，关于打印处理器
- 自定义打印处理器 WDK
- 打印处理器 WDK，数据类型
- 数据类型 WDK 打印处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3a3b9b373705285a6202eebf71e09aea2f58e1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796669"
---
# <a name="introduction-to-print-processors"></a>打印处理器简介





打印处理器是用户模式 Dll，负责将打印作业的假脱机数据转换为可发送到 *打印监视器* 的格式。 它们还负责处理应用程序请求以暂停、恢复和取消打印作业。

打印作业的假脱机数据包含在假脱机文件中。 打印处理器读取文件，对数据流执行转换操作，并将转换后的数据写入到后台处理程序。 然后，后台处理程序将数据流发送到相应的打印监视器。

Microsoft Windows 2000 和更高版本包含下表中列出的打印处理器。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>打印处理器</th>
<th>输入数据类型</th>
<th>输出数据类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Localspl.dll *</p></td>
<td><p>EMF</p>
<p>RAW</p>
<p>TEXT</p></td>
<td><p>RAW</p></td>
</tr>
<tr class="even">
<td><p>Sfmpsprt.dll</p></td>
<td><p>PSCRIPT1</p></td>
<td><p>RAW</p></td>
</tr>
</tbody>
</table>

 

\* 从 Windows 2000 开始，Localmon.dll 和 Winprint.dll 包含在 Localspl.dll 中。

有关数据类型的信息，请参阅以下主题：

[EMF 数据类型](emf-data-type.md)

[RAW 数据类型](raw-data-type.md)

[文本数据类型](text-data-type.md)

[PSCRIPT1 数据类型](pscript1-data-type.md)

您可以创建自定义的打印处理器来支持 Windows 2000 或更高版本的操作系统版本不支持的数据类型。 你还可以提供支持一个或多个支持的数据类型的自定义打印处理器，从而允许你修改提供的打印处理器提供的功能。

打印处理器与驱动程序安装过程中的打印机驱动程序相关联，因此，多个支持相同数据类型的打印处理器可以共存。 有关详细信息，请参阅 [安装打印处理器](installing-a-print-processor.md)。

**注意**   编译打印处理器时，使用 "定义 UNICODE" 设置 Unicode 标志 \# 。 例如，打印处理器代码只应使用 LPWSTR 类型的宽字符串。

 

 

 




