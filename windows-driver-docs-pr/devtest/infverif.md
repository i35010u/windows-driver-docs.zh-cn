---
title: InfVerif
description: '了解 InfVerif ( # A0) 工具。 你可以使用此工具来测试驱动程序 INF 文件，或查明 INF 文件是否是通用的。'
ms.assetid: 6F565E1C-C6FC-4637-B476-FE4E4672CCC3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aea0f0827614e5e4b2cd44ae182e73142d005fe
ms.sourcegitcommit: f1d6c2d0cdbecdc69ba65ed3b530755fc73c8e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590377"
---
# <a name="infverif"></a>InfVerif


InfVerif ( # A0) 是可用于测试驱动程序 INF 文件的工具。 除了报告 INF 语法问题外，该工具还报告 INF 文件是否是通用的。

> [!NOTE]
> InfVerif 取代了 ChkINF 工具。

当你使用 Windows 驱动程序 (工具包在 Microsoft Visual Studio 2017 中构建驱动程序时) 10，编译器会在生成过程中自动运行该工具。 或者，可以从命令行运行 InfVerif.exe 工具。

验证工具是 WDK 10 安装的一部分，可在 \\ wdk 10 安装的 tools 子目录中找到，c： \\ Program Files (x86) \\ Windows 工具包 \\ 10 \\ 工具中 \\ 。

InfVerif 工具将报告以下类型的错误/警告：

-   **错误/警告** (1200-1299) ：这些问题不会阻止安装驱动程序包，但会表明在安装驱动程序时，不会执行 INF 的特定行。

-   **导致 INF 非通用的问题。**  (1300-1309) 

-   **警告** (2000-2999) ：这些问题始终报告为警告。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="running-infverif-from-the-command-line.md" data-raw-source="[Running InfVerif from the command line](running-infverif-from-the-command-line.md)">从命令行运行 InfVerif</a></p></td>
<td align="left"><p>本主题列出了从命令行运行 InfVerif.exe 时可用的选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="inf-validation-errors-and-warnings.md" data-raw-source="[INF Validation Errors and Warnings](inf-validation-errors-and-warnings.md)">INF 验证错误和警告</a></p></td>
<td align="left"><p>本主题介绍在 Visual Studio 执行的自动 INF 验证或运行 InfVerif 工具时可能出现的驱动程序安装错误和警告。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[通用 Windows 驱动程序入门](../develop/getting-started-with-windows-drivers.md)

[Using a Universal INF File](../install/using-a-universal-inf-file.md)（使用通用 INF 文件）

 

