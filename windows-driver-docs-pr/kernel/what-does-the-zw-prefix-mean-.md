---
title: Zw 前缀的含义是什么
description: Zw 前缀的含义是什么
ms.assetid: 9529cce9-9c46-4906-854d-d0aef9118a90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1056a684884a13e164a2d722c619c4aa5ce2def8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184395"
---
# <a name="what-does-the-zw-prefix-mean"></a>Zw 前缀是什么？


Windows native 系统服务例程的名称以前缀 **Nt** 和 **Zw**开头。 **Nt**前缀是 Windows Nt 的缩写，但**Zw**前缀没有任何意义。 已选择**Zw** ，以避免潜在的与其他 api 的命名冲突，其中部分是避免使用将来可能需要的任何有用的双字母前缀。

许多 [Windows 驱动程序支持例程](/windows-hardware/drivers/ddi/index) 的名称以两个或三个字母开头。 这些前缀指示哪些内核模式系统组件实现了例程。 下表包含一些示例。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>前缀</th>
<th>内核组件</th>
<th>示例例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ilm-cm</strong></p></td>
<td><p>配置管理器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex" data-raw-source="[&lt;strong&gt;CmRegisterCallbackEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)"><strong>CmRegisterCallbackEx</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>例如</strong></p></td>
<td><p>Executive</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool" data-raw-source="[&lt;strong&gt;ExAllocatePool&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)"><strong>ExAllocatePool</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Hal</strong></p></td>
<td><p>硬件抽象层</p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)" data-raw-source="[&lt;strong&gt;HalGetAdapter&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))"><strong>HalGetAdapter</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>排</strong></p></td>
<td><p>I/o 管理器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ke</strong></p></td>
<td><p>内核核心</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>月</strong></p></td>
<td><p>内存管理器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages" data-raw-source="[&lt;strong&gt;MmUnlockPages&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)"><strong>MmUnlockPages</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ob</strong></p></td>
<td><p>对象管理器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)"><strong>ObReferenceObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>邮箱</strong></p></td>
<td><p>电源管理器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate" data-raw-source="[&lt;strong&gt;PoSetPowerState&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)"><strong>PoSetPowerState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>费</strong></p></td>
<td><p>事务管理器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmcommittransaction" data-raw-source="[&lt;strong&gt;TmCommitTransaction&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-tmcommittransaction)"><strong>TmCommitTransaction</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Nt</strong> 和 <strong>Zw</strong></p></td>
<td><p>本机系统服务</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157250" data-raw-source="[NtCreateFile](https://go.microsoft.com/fwlink/p/?linkid=157250)">NtCreateFile</a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)"> <strong>ZwCreateFile</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

