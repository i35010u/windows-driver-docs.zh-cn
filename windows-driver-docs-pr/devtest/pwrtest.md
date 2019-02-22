---
title: PwrTest
description: 电源管理测试工具 (PwrTest) 是一个测试工具，开发人员、 测试人员和系统集成商来执行和记录系统从电源管理信息。
ms.assetid: 8c242d61-6c5b-44d9-84d1-f78ef9a56a6d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 097114a7782c79d216a3a2adfb0506ad28f267ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545507"
---
# <a name="pwrtest"></a>PwrTest


电源管理测试工具 (PwrTest) 是一个测试工具，开发人员、 测试人员和系统集成商来执行和记录系统从电源管理信息。 PwrTest 可用于自动执行休眠和恢复转换并记录处理器电源管理和电池信息从系统一段时间内。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在何处可以下载 PwrTest？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PwrTest.exe 包含 Microsoft Windows Driver Kit (WDK) 中。 有关获取 WDK 的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Driver Kit Downloads]( https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows 驱动程序工具包下载</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrunningpwrtestspanspan-idrunningpwrtestspanspan-idrunningpwrtestspanrunning-pwrtest"></a><span id="Running_PwrTest"></span><span id="running_pwrtest"></span><span id="RUNNING_PWRTEST"></span>运行 PwrTest


PwrTest (PwrTest.exe) 的功能完备的日志记录以及命令行接口。 PwrTest 都能够为 Microsoft Windows 测试技术 (WTL) 和 XML 文件格式的日志记录信息。

PwrTest 功能分为方案。 有关这些方案的信息，请参阅[PwrTest 方案](pwrtest-scenarios.md)。

**若要运行 Pwrtest**

1.  若要能够使用所有 PwrTest 方案，必须先设置测试计算机以用于使用 Visual Studio 和 WDK 测试。 有关详细信息，请参阅[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)，或[预配计算机，以使驱动程序部署和测试 (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/hh698272)。

    某些情况下需要是一部分的 Windows 驱动程序测试框架 (WDTF) 的电源按钮驱动程序。 预配的系统，使用 Visual Studio 和 WDK 测试时，会自动安装 WDTF （和包含的电源按钮驱动程序）。

2.  PwrTest.exe 随 WDK。 若要在测试计算机上运行 Pwrtest，必须从安装 WDK 的计算机复制 PwrTest.exe。

    您可以在 Windows 驱动程序工具包工具目录中查找 PwrTest.exe (例如，c:\\Program Files (x86)\\Windows 工具包\\*&lt;版本&gt;* \\工具\\*&lt;平台&gt;*\\PwrTest.exe)。

3.  你已设置的测试计算机上使用提升的权限打开命令提示符窗口 (**以管理员身份运行**) 并导航到复制 PwrTest.exe 的目录。

    **示例**

    ```
    pwrtest /? 
    ```

    ```
    pwrtest /battery /c:4 /i:1000
    ```

    有关详细信息，请参阅[PwrTest 语法](pwrtest-syntax.md)并[PwrTest 方案](pwrtest-scenarios.md)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[PwrTest 语法](pwrtest-syntax.md)

[PwrTest 日志文件](pwrtest-log-file.md)

[PwrTest 方案](pwrtest-scenarios.md)

[预配的计算机的驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)

[预配的计算机的驱动程序部署和测试 (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/hh698272)

 

 






