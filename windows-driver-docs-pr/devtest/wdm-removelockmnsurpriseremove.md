---
title: RemoveLockMnSurpriseRemove 规则 (wdm)
description: RemoveLockMnSurpriseRemove 规则验证是否正确使用对 IoAcquireRemoveLock 和 IoReleaseRemoveLockAndWait 调用时处理 IRP\_MJ\_PNP 与 MinorFunction IRP\_MN\_SUPRISE\_删除。
ms.assetid: 536D5658-F229-456F-979C-96BF7384ADE5
ms.date: 05/21/2018
keywords:
- RemoveLockMnSurpriseRemove 规则 (wdm)
topic_type:
- apiref
api_name:
- RemoveLockMnSurpriseRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b729e5d137c0aa365be29a7f2940dfe81ae41ec5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363227"
---
# <a name="removelockmnsurpriseremove-rule-wdm"></a>RemoveLockMnSurpriseRemove 规则 (wdm)


**RemoveLockMnSurpriseRemove**规则验证的调用[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)并[ **IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)处理 IRP 时正确使用\_MJ\_PNP 与 MinorFunction IRP\_MN\_SUPRISE\_删除。 该驱动程序应转发堆栈的下层 IRP 之前获取的删除锁定。

此规则仅适用于 FDO 和 FIDO 驱动程序。

例如，考虑筛选器驱动程序、 FDO 和一个 PDO 组成的即插即用驱动程序堆栈。

PnP 管理器将发送通过堆栈查询删除。 FDO 启用空闲系统运行时。 FDO 决定幂下在查询中删除状态下，因此它会请求 d0 IRP。 D0 IRP 到达之前，PnP 管理器将即插即用删除 IRP 和筛选器驱动程序处理 IRP 发送。 筛选器驱动程序从堆栈中分离，并清除其状态。 D0 到达堆栈的顶部，但筛选器驱动程序不会发送它在堆栈的下层因为它具有任何上下文或数据来了解哪个不再发送。 FDO 等待 d0 IRP 到达，但 IRP 永远也不会挂起。

**若要避免此错误**

1.  设备与设备堆栈之前[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204) IRP 转发下以下 IRP 类型的堆栈之前必须成功：

    -   IRP\_MN\_查询\_删除
    -   IRP\_MN\_SUPRISE\_REMOVAL
    -   IRP\_MN\_REMOVE\_DEVICE

2.  [**IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)调用之前，应调用[ **IoDetachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549087)或者[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083). （这可确保在设备驱动程序会释放所有的删除锁定）。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>RemoveLockMnSurpriseRemove</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
[**RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





