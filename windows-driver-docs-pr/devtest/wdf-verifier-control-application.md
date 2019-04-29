---
title: WDF 验证程序控制应用程序
description: Windows 驱动程序框架 (WDF) 验证程序控制应用程序 (WdfVerifier.exe) 是一个用于调试 KMDF 和 UMDF 驱动程序工具。
ms.assetid: 896b63db-69c6-4fcb-a50f-0c4aed394b0b
keywords:
- WDF 验证程序控件应用程序 WDK，功能
- WDF 验证程序 WDK
- 工具 WDK，验证驱动程序
- 测试驱动程序 WDK WDF
- 调试驱动程序 WDK WDF
- 验证驱动程序 WDK WDF
- 验证程序 WDK KMDF
- 验证程序 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4ba2fc80c9bece971089a9411954ad0728750fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380453"
---
# <a name="wdf-verifier-control-application"></a>WDF 验证程序控制应用程序


Windows 驱动程序框架 (WDF) 验证程序控制应用程序 (WdfVerifier.exe) 是一个用于调试内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序工具。 该工具可用于在计算机上，并对其调试器设置进行更改的驱动程序的快速评估。

本文档介绍随附的 Windows Driver Kit (WDK) 8.1 的应用程序的版本中的选项。

**重要**若要使用 WDF 验证程序，必须具有管理权限的计算机上。

 

### <a name="span-idwdfverifierfeaturesspanspan-idwdfverifierfeaturesspanwhat-can-i-do-with-it"></a><span id="wdf_verifier_features"></span><span id="WDF_VERIFIER_FEATURES"></span>我如何使用它？

-   获取有关所有 WDF 驱动程序的计算机上的快速信息。 驱动程序或设备，可以组织列表。
-   用于调试 WDF 驱动程序管理注册表设置。
-   查看 UMDF 驱动程序主机进程和其托管的驱动程序。
-   管理诊断输出。
-   手动或自动启动用户模式下调试会话。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p>本主题提供有关 WDF 验证程序的详细的信息<strong>WDF 驱动程序</strong>页。 此页面列出了所有 WDF 驱动程序的计算机上，并且可以更改其验证设置和使用它们的设备的设置。 如果您感兴趣的特定驱动程序下，从这里开始。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="devices-using-wdf-tab.md" data-raw-source="[Devices Using WDF Tab](devices-using-wdf-tab.md)">使用 WDF 选项卡上的设备</a></p></td>
<td align="left"><p>本主题讨论了 WDF Verifier<strong>使用 WDF 设备</strong>页。 此页列出了使用 WDF 驱动程序的所有设备。 在突出显示设备，可以看到突出显示设备的 WDF 驱动程序堆栈。 在此屏幕中，您还可以更改验证设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="global-wdf-settings-tab.md" data-raw-source="[Global WDF Settings Tab](global-wdf-settings-tab.md)">全局 WDF 设置选项卡</a></p></td>
<td align="left"><p>本主题提供有关 WDF 验证程序的详细的信息<strong>全局 WDF 设置</strong>页。 此页提供了全局 （系统范围内） WDF 验证选项，并显示与托管驱动程序 UMDF 主机进程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="umdf-settings-test-use-only-tab.md" data-raw-source="[UMDF Settings (Test Use Only) Tab](umdf-settings-test-use-only-tab.md)">UMDF 设置 （仅供测试使用） 选项卡</a></p></td>
<td align="left"><p>本主题详细介绍了 WDF Verifier <strong>UMDF 设置 （测试使用仅限）</strong>页。 在此页上，您可以更改可帮助测试一个或多个 UMDF 驱动程序的整体系统的设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="my-preferences-tab.md" data-raw-source="[My Preferences Tab](my-preferences-tab.md)">我的首选项选项卡</a></p></td>
<td align="left"><p>本主题介绍了 WDF Verifier<strong>我的首选项</strong>页。 在此页上，可以设置首选项对于某些控件面板的功能。</p></td>
</tr>
</tbody>
</table>

 

 

 





