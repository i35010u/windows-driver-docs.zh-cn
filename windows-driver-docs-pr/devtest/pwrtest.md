---
title: PwrTest
description: 电源管理测试工具（PwrTest）是一种测试工具，可让开发人员、测试人员和系统集成商测试系统中的电源管理信息。
ms.assetid: 8c242d61-6c5b-44d9-84d1-f78ef9a56a6d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61078d41b80e86f6476b0304749eba52c40162b0
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769407"
---
# <a name="pwrtest"></a>PwrTest


电源管理测试工具（PwrTest）是一种测试工具，可让开发人员、测试人员和系统集成商测试系统中的电源管理信息。 你可以使用 PwrTest 自动执行睡眠和恢复转换，并记录系统在一段时间内的处理器电源管理和电池信息。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在哪里可以下载 PwrTest？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PwrTest 包含在 Microsoft Windows 驱动程序工具包（WDK）中。 有关获取 WDK 的信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Driver Kit Downloads](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)">Windows 驱动程序工具包下载</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrunning_pwrtestspanspan-idrunning_pwrtestspanspan-idrunning_pwrtestspanrunning-pwrtest"></a><span id="Running_PwrTest"></span><span id="running_pwrtest"></span><span id="RUNNING_PWRTEST"></span>运行 PwrTest


PwrTest （PwrTest）具有强健的日志记录和命令行界面。 PwrTest 可以将信息记录到 Microsoft Windows 测试技术（WTL）和 XML 文件格式。

PwrTest 功能分为不同方案。 有关这些方案的详细信息，请参阅[PwrTest 方案](pwrtest-scenarios.md)。

**运行 Pwrtest**

1.  为了能够使用所有 PwrTest 方案，你必须首先设置测试计算机，以便使用 Visual Studio 和 WDK 进行测试。 有关详细信息，请参阅为[驱动程序部署和测试预配计算机（wdk 8.1）](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)，或[设置用于驱动程序部署和测试的计算机（wdk 8）](https://docs.microsoft.com/previous-versions/hh698272(v=vs.85))。

    某些方案需要电源按钮驱动程序，该驱动程序是 Windows 驱动程序测试框架（WDTF）的一部分。 使用 Visual Studio 和 WDK 预配系统进行测试时，会自动安装 WDTF （和随附的电源按钮驱动程序）。

2.  PwrTest 随 WDK 一起安装。 若要在测试计算机上运行 Pwrtest，必须从安装了 WDK 的计算机复制 PwrTest。

    您可以在 windows 驱动程序工具包工具目录中找到 PwrTest （例如，C： \\ Program Files （x86） \\ windows 工具包 \\ * &lt; 版本 &gt; * \\ 工具 \\ * &lt; 平台 &gt; * \\ PwrTest）。

3.  在已设置的测试计算机上，使用提升的权限（以**管理员身份运行**）打开 "命令提示符" 窗口，并导航到 PwrTest 复制到的目录。

    **示例**

    ```
    pwrtest /? 
    ```

    ```
    pwrtest /battery /c:4 /i:1000
    ```

    有关详细信息，请参阅[PwrTest 语法](pwrtest-syntax.md)和[PwrTest 方案](pwrtest-scenarios.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PwrTest 语法](pwrtest-syntax.md)

[PwrTest 日志文件](pwrtest-log-file.md)

[PwrTest 方案](pwrtest-scenarios.md)

[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)

[预配用于驱动程序部署和测试的计算机（WDK 8）](https://docs.microsoft.com/previous-versions/hh698272(v=vs.85))

 

 






