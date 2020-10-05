---
title: Zw 前缀的含义是什么
description: Zw 前缀的含义是什么
ms.assetid: 9529cce9-9c46-4906-854d-d0aef9118a90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 38da09c401defa1097256c27c62cae21911ae715
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733943"
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
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex" data-raw-source="[&lt;strong&gt;CmRegisterCallbackEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)"><strong>CmRegisterCallbackEx</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>例如</strong></p></td>
<td><p>Executive</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool" data-raw-source="[&lt;strong&gt;ExAllocatePool&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)"><strong>ExAllocatePool</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Hal</strong></p></td>
<td><p>硬件抽象层</p></td>
<td><p><a href="/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)" data-raw-source="[&lt;strong&gt;HalGetAdapter&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))"><strong>HalGetAdapter</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>排</strong></p></td>
<td><p>I/o 管理器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ke</strong></p></td>
<td><p>内核核心</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>月</strong></p></td>
<td><p>内存管理器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages" data-raw-source="[&lt;strong&gt;MmUnlockPages&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)"><strong>MmUnlockPages</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ob</strong></p></td>
<td><p>对象管理器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)"><strong>ObReferenceObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>邮箱</strong></p></td>
<td><p>电源管理器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate" data-raw-source="[&lt;strong&gt;PoSetPowerState&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)"><strong>PoSetPowerState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>费</strong></p></td>
<td><p>事务管理器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-tmcommittransaction" data-raw-source="[&lt;strong&gt;TmCommitTransaction&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-tmcommittransaction)"><strong>TmCommitTransaction</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Nt</strong> 和 <strong>Zw</strong></p></td>
<td><p>本机系统服务</p></td>
<td><p><a href="/windows/win32/api/winternl/nf-winternl-ntcreatefile" data-raw-source="[NtCreateFile](/windows/win32/api/winternl/nf-winternl-ntcreatefile)">NtCreateFile</a>和<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)"> <strong>ZwCreateFile</strong></a></p></td>
</tr>
</tbody>
</table>

