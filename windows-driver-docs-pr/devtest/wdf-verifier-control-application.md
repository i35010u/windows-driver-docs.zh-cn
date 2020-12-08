---
title: WDF 验证程序控制应用程序
description: 'Windows 驱动程序框架 (WDF) 验证器控件应用程序 ( # A0) 是用于调试 KMDF 和 UMDF 驱动程序的工具。'
keywords:
- WDF 验证器控件应用程序 WDK，功能
- WDF 验证程序 WDK
- 工具 WDK，验证驱动程序
- 测试驱动程序 WDK WDF
- 调试驱动程序 WDK WDF
- 验证驱动程序 WDK WDF
- 验证程序 WDK KMDF
- 验证程序 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4923c420e6280f85afc6ee8b99480679dca38a7f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823337"
---
# <a name="wdf-verifier-control-application"></a>WDF 验证程序控制应用程序


Windows 驱动程序框架 (WDF) 验证器控件应用程序 ( # A0) 是一种用于调试 Kernel-Mode 驱动程序框架 (KMDF) 和 User-Mode UMDF (驱动程序的工具。 您可以使用该工具快速评估计算机上的驱动程序，并对其调试程序设置进行更改。

本文档介绍了在 Windows 驱动程序工具包 (中作为 Windows 驱动程序工具包的一部分提供的选项，) 8.1。

**重要提示**  若要使用 WDF 验证程序，您必须在计算机上具有管理权限。

 

### <a name="span-idwdf_verifier_featuresspanspan-idwdf_verifier_featuresspanwhat-can-i-do-with-it"></a><span id="wdf_verifier_features"></span><span id="WDF_VERIFIER_FEATURES"></span>我该怎么办？

-   获取有关计算机上所有 WDF 驱动程序的快速信息。 可以按驱动程序或设备组织列表。
-   管理用于调试 WDF 驱动程序的注册表设置。
-   查看 UMDF 驱动程序主机的进程和驱动程序。
-   管理诊断输出。
-   手动或自动启动用户模式调试会话。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p><a href="wdf-drivers-tab.md" data-raw-source="[WDF Drivers Tab](wdf-drivers-tab.md)">WDF 驱动程序选项卡</a></p></td>
<td align="left"><p>本主题提供有关 WDF 验证 <strong>程序的 Wdf 驱动程序</strong> 页面的详细信息。 此页面列出计算机上的所有 WDF 驱动程序，你可以更改其验证设置以及使用这些驱动程序的设备的设置。 如果你对特定驱动程序感兴趣，请从此处开始。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="devices-using-wdf-tab.md" data-raw-source="[Devices Using WDF Tab](devices-using-wdf-tab.md)">使用 WDF 选项卡的设备</a></p></td>
<td align="left"><p>本主题讨论 <strong>使用 wdf</strong> 的 wdf 验证程序的设备。 此页列出了使用 WDF 驱动程序的所有设备。 突出显示设备时，将看到突出显示的设备的 WDF 驱动程序堆栈。 你还可以通过此屏幕更改验证设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="global-wdf-settings-tab.md" data-raw-source="[Global WDF Settings Tab](global-wdf-settings-tab.md)">全局 WDF 设置选项卡</a></p></td>
<td align="left"><p>本主题提供有关 WDF 验证器的 " <strong>全局 WDF 设置</strong> " 页的详细信息。 此页显示全局 (系统范围内) WDF 验证选项，并显示具有托管驱动程序的 UMDF 主机进程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="umdf-settings-test-use-only-tab.md" data-raw-source="[UMDF Settings (Test Use Only) Tab](umdf-settings-test-use-only-tab.md)">UMDF 设置（仅供测试）选项卡</a></p></td>
<td align="left"><p>本主题详细说明 WDF 验证程序的 <strong>UMDF 设置 (测试仅) </strong> 页面。 在此页上，你可以更改设置，以帮助使用一个或多个 UMDF 驱动程序来测试整个系统。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="my-preferences-tab.md" data-raw-source="[My Preferences Tab](my-preferences-tab.md)">我的首选项选项卡</a></p></td>
<td align="left"><p>本主题介绍 WDF 验证器的 <strong>"我的首选项"</strong> 页。 在此页上，您可以为某些 "控制面板" 功能设置首选项。</p></td>
</tr>
</tbody>
</table>

 

 

 





