---
title: InfVerif
description: InfVerif (InfVerif.exe) 是一种工具，可用于测试的驱动程序 INF 文件。 除了报告 INF 语法问题，该工具将报告 INF 文件是否通用。
ms.assetid: 6F565E1C-C6FC-4637-B476-FE4E4672CCC3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaed883fbba4d9b9186829d0af0a269fd4763803
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545965"
---
# <a name="infverif"></a>InfVerif


InfVerif (InfVerif.exe) 是一种工具，可用于测试的驱动程序 INF 文件。 除了报告 INF 语法问题，该工具将报告 INF 文件是否通用。

> [!NOTE]
> InfVerif 将替代 ChkINF 工具。

生成的驱动程序在 Microsoft Visual Studio 2017 中使用 Windows Driver Kit (WDK) 10 时，编译器运行该工具自动生成过程的一部分。 或者，您可以从命令行运行 InfVerif.exe 工具。

验证工具是 WDK 10 安装的一部分，可在\\WDK 10 安装，工具子目录 c:\\程序 Files(x86)\\Windows 工具包\\10\\工具\\.

InfVerif 工具将报告以下类型的错误/警告：

-   **错误/警告**(1200年 1299):这些问题并防止驱动程序包安装，但它们指示，在 INF 的特定行时不会被执行安装的驱动程序。

-   **使非通用 INF 的问题。** (1300-1309)

-   **警告**(2000年-2999):这些问题会始终报告为警告。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>在本部分中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="running-infverif-from-the-command-line.md" data-raw-source="[Running InfVerif from the command line](running-infverif-from-the-command-line.md)">从命令行运行 InfVerif</a></p></td>
<td align="left"><p>本主题列出了从命令行运行 InfVerif.exe 时可用的选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="inf-validation-errors-and-warnings.md" data-raw-source="[INF Validation Errors and Warnings](inf-validation-errors-and-warnings.md)">INF 验证错误和警告</a></p></td>
<td align="left"><p>本主题介绍驱动程序安装错误和警告可以显示作为自动 INF 验证结果，Visual Studio 的执行，或 InfVerif 工具的运行时。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[安装通用 Windows 驱动程序](https://msdn.microsoft.com/windows-drivers/develop/installing_a_universal_driver)

[使用通用 INF 文件](https://msdn.microsoft.com/library/windows/hardware/dn941087)

 

 






