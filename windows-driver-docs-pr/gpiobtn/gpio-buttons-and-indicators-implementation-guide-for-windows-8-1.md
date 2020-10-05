---
title: GPIO 按钮和指示器实现指南
description: Windows 8 通过 HID 微型端口类驱动程序引入了对常规 I/O (GPIO) 按钮和指示器的支持。
ms.assetid: E073E15A-7068-43D0-9DBA-7DD2E7FE2993
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 60602118f2672e873db92d59335bf67e1972a303
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733292"
---
# <a name="gpio-buttons-and-indicators-implementation-guide"></a>GPIO 按钮和指示器实现指南


Windows 8 通过 HID 微型端口类驱动程序引入了对常规 I/O (GPIO) 按钮和指示器的支持。 目标是以标准化方式提供对主要按钮（电源、Windows、音量和旋转锁）的支持，另外还介绍了已关联的相应 Windows 工程指南 (WEG)。 Windows 8.1 专注于增强端到端用户体验的质量以及统一各种创新性外形规格的行为。

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
<td align="left"><p><a href="state-indicators.md" data-raw-source="[State indicators](state-indicators.md)">状态指示器</a></p></td>
<td align="left"><p>本部分介绍模式和停靠指示器的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="physical-buttons.md" data-raw-source="[Physical buttons](physical-buttons.md)">物理按钮</a></p></td>
<td align="left"><p>使用硬件按钮，用户可以执行很多不具有便利用户界面的常见任务。 对于本部分中所述的方案，硬件按钮通常用于在用户无法使用的情况下出现的任务，如改装或清单。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="interface-implementation-guidance.md" data-raw-source="[Interface implementation guidance](interface-implementation-guidance.md)">接口实现指南</a></p></td>
<td align="left"><p>本部分提供有关接口实现的指南。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="code-samples.md" data-raw-source="[Code samples](code-samples.md)">代码示例</a></p></td>
<td align="left"><p>本部分包含用于接口实现的代码示例和示例说明符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="implement-the-unattended-windows-setup-setting.md" data-raw-source="[Implement the unattended Windows Setup setting](implement-the-unattended-windows-setup-setting.md)">实现无人参与 Windows 安装程序设置</a></p></td>
<td align="left"><p>本主题介绍如何设置无人参与的 Windows 安装程序组件设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="logging-and-investigations.md" data-raw-source="[Logging and investigations](logging-and-investigations.md)">日志记录和调查</a></p></td>
<td align="left"><p>本主题介绍 GPIO 实现的日志记录和调查。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="running-test-passes.md" data-raw-source="[Running test passes](running-test-passes.md)">运行测试通过</a></p></td>
<td align="left"><p>MITT 平台通过提供测试自动化和用于自定义为目标调查发送的 GPIO 模式的选项来测试 GPIO 按钮。</p></td>
</tr>
</tbody>
</table>

 

作为 Windows 8.1 投资的一部分， **msgpio** 按钮驱动程序带来了重要的增强功能：

-   增加了日志记录以加速调查。
-   改进了同步和错误处理以增强可靠性。
-   新的 ConvertibleSlateMode [无人参与 Windows 安装程序](/previous-versions/windows/it-pro/windows-8.1-and-8/ff699026(v=win.10)) 在非 GPIO 便携式计算机上用于静态地将模式设置为便携式计算机作为 OEM 映像自定义的一部分。

有关 GPIO 按钮和指标实现的问题，请发送电子邮件至 Microsoft 支持组，网址为 dockingsupport@microsoft.com 。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[电源按钮行为和实现](/collaborate/connect-redirect?DownloadID=47452)  
[连接备用唤醒源](/collaborate/connect-redirect?DownloadID=49891)  
[ACPI 设计指南](/collaborate/connect-redirect?DownloadID=48755)  
[GetSystemMetrics 函数](/windows/win32/api/winuser/nf-winuser-getsystemmetrics)  
[Windows 8 中的键盘增强功能](/previous-versions/windows/hardware/design/dn613956(v=vs.85))  
[Windows 硬件兼容性计划](/windows-hardware/design/compatibility/index)  
[Windows 桌面应用程序的认证要求](/windows/win32/win_cert/certification-requirements-for-windows-desktop-apps)  
[基于 I i2c 的 HID](../hid/hid-over-i2c-guide.md)  
[MITT 中的 GPIO 测试](../spb/gpio-tests-in-mitt.md)  
[Windows 系统映像管理器技术参考](/previous-versions/windows/it-pro/windows-vista/cc722301(v=ws.10))  
[无人参与 Windows 安装参考](/previous-versions/windows/it-pro/windows-8.1-and-8/ff699026(v=win.10))  
[Windows 驱动程序工具包 (WDK) 8。1](https://go.microsoft.com/fwlink/p/?linkid=310164)