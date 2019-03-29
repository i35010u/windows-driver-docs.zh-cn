---
title: 静态驱动程序验证程序
description: 静态驱动程序验证程序
ms.assetid: 74feeb16-387c-4796-987a-aff3fb79b556
keywords:
- 验证驱动程序 WDK、 Static Driver Verifier
- 驱动程序验证 WDK、 Static Driver Verifier
- WDK 的 static Driver Verifier
- StaticDV WDK
- SDV WDK
- 路径 WDK SDV
- 编译时静态验证工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1c7d189c43fa9d21405ba2ce72d8a13137ea69f
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464211"
---
# <a name="static-driver-verifier"></a>静态驱动程序验证程序


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>用途</strong></p>
<p>Static Driver Verifier （也称为"StaticDV"或"SDV"） 是一个静态验证工具，系统化地分析 Windows 内核模式驱动程序的源代码。 SDV 是一种编译时工具，能够发现缺陷和驱动程序中的设计问题。 根据一组接口规则和操作系统的模型，SDV 确定驱动程序是否正确交互与 Windows 操作系统内核。</p>
<p></p>
 
<p><strong>安装</strong></p>
<p>Static Driver Verifier 可作为的一部分<a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk">Windows Driver Kit (WDK)</a>和独立企业 WDK 中完整的 WDK 体验。  此外，<a href="https://www.microsoft.com/en-us/download/details.aspx?id=40784">适用于 Visual Studio 2013 的 Visual c + + 可再发行组件包</a>并<a href="https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads">Visual Studio 2017 的 Visual c + + 可再发行组件包</a>所需的 SDV 来运行。  
<p></p>对于版本的 WDK 为 Windows 10，版本 1809年或更早版本中可用的 SDV<a href="https://my.visualstudio.com/Downloads?pid=1452">适用于 Visual Studio 2012 的 Visual c + + 可再发行组件包</a>应安装而不是 2017年包。
<p></p>
 
</div>
<p><strong>Visual Studio Integration</strong></p>
<p>Static Driver Verifier 集成到 Visual Studio。 在 Visual Studio 驱动程序项目，可以运行静态分析。 可以启动、 配置和控制从 Static Driver Verifier<strong>驱动程序</strong>Visual Studio 菜单中的。</p>
<p><strong>Static Driver Verifier 文档</strong></p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/develop/static-driver-verifier-known-issues">Static Driver Verifier 的已知问题</a>
<p>Static Driver Verifier 列出了最新的已知的问题</p>
<a href="using-static-driver-verifier-to-find-defects-in-drivers.md" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](using-static-driver-verifier-to-find-defects-in-drivers.md)">使用 Static Driver Verifier 来查找驱动程序中的缺陷</a>
<p>告诉您需要开始分析驱动程序代码在 Visual Studio 环境中。</p>
<a href="-static-driver-verifier-commands--msbuild-.md" data-raw-source="[Static Driver Verifier commands (MSBuild)](-static-driver-verifier-commands--msbuild-.md)">静态 Driver Verifier 命令 (MSBuild)</a>
<p>列出要使用的 Visual Studio 命令提示符窗口中运行 SDV 的 MSBuild 命令。</p>
<a href="introducing-static-driver-verifier.md" data-raw-source="[Introducing Static Driver Verifier](introducing-static-driver-verifier.md)">引入的 Static Driver Verifier</a>
<p>提供了静态分析工具的概述。</p>
<a href="using-static-driver-verifier.md" data-raw-source="[Using Static Driver Verifier](using-static-driver-verifier.md)">使用 Static Driver Verifier</a>
<p>提供了有关使用和配置的静态分析工具的详细信息。</p>
<a href="static-driver-verifier-report.md" data-raw-source="[Static Driver Verifier Report](static-driver-verifier-report.md)">Static Driver Verifier 报表</a>
<p>描述的查看器显示的静态代码分析详细的跟踪。</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff552840" data-raw-source="[Static Driver Verifier Rules](https://msdn.microsoft.com/library/windows/hardware/ff552840)">Static Driver Verifier 规则</a>
<p>规则定义所需的正确驱动程序模型和操作系统的内核接口之间的交互。</p>
<a href="static-driver-verifier-reference.md" data-raw-source="[Static Driver Verifier Reference](static-driver-verifier-reference.md)">Static Driver Verifier 引用</a>
<p>提供了有关函数的角色类型、 SDV 配置文件、 错误和警告消息的参考信息。</p></td>
<td align="left"><p><em>静态分析可以减少缺陷的最多六篇文章构成身份 ！</em></p>
<p>— Capers Jones，软件工作效率组</p>
<p><strong>Windows 驱动程序代码中查找错误</strong></p>
<p>Microsoft 使用 SDV 来测试是 Microsoft Windows 操作系统附带的内核模式驱动程序，并在 WDK 中测试的示例驱动程序。 在 Windows 8 的发布之前, Microsoft 使用 SDV 来查找并修复 127 潜在的严重 bug。</p>
<p>通过对特定驱动程序模型使用 DDI 符合性规则，SDV 可以验证正确的驱动程序行为。 例如，SDV 可以验证该驱动程序：</p>
<ul>
<li><p>在正确的 IRQL 调用函数</p></li>
<li><p>获取和释放锁正确的顺序</p></li>
<li><p>正确使用函数，用于处理 I/O 请求数据包 (IRP)</p></li>
</ul>
<p>SDV 检查通过驱动程序代码的所有可能路径。 它旨在彻底的测试中甚至不太可能会遇到的晦涩路径中查找出现严重的错误。</p>
<p><strong>资源</strong></p>
<p>SDV 可以验证的驱动程序相关的特定信息，请参阅<a href="supported-drivers.md" data-raw-source="[Supported Drivers](supported-drivers.md)">支持的驱动程序</a>。</p>
<p>有关详细信息和有关使用 Static Driver Verifier 的提示，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=154232" data-raw-source="[Static Driver Tools blog](https://go.microsoft.com/fwlink/p/?linkid=154232)">静态驱动程序工具博客</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 

