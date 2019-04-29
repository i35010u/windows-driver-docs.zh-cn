---
title: Zw 前缀是什么意思
description: Zw 前缀是什么意思
ms.assetid: 9529cce9-9c46-4906-854d-d0aef9118a90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e2e5aa0bdff701eb7eda6713a6fce120902b0697
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391434"
---
# <a name="what-does-the-zw-prefix-mean"></a>Zw 前缀是什么？


Windows 本机系统服务例程具有以前缀开头的名称**Nt**并**Zw**。 **Nt**前缀是 Windows NT 的缩写，但**Zw**前缀没有任何意义。 **Zw**部分以避免与其他 Api 的潜在命名冲突并一定程度上避免使用任何可能有用的两个字母前缀可能需要在将来的选择。

许多[Windows 驱动程序支持例程](https://msdn.microsoft.com/library/windows/hardware/ff544200)具有两个或三个字母的前缀开头的名称。 这些前缀表示的内核模式系统组件实现例程。 下表包含一些示例。

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
<td><p><strong>Cm</strong></p></td>
<td><p>配置管理器</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541921" data-raw-source="[&lt;strong&gt;CmRegisterCallbackEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541921)"><strong>CmRegisterCallbackEx</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Ex</strong></p></td>
<td><p>高级管理人员</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544501" data-raw-source="[&lt;strong&gt;ExAllocatePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544501)"><strong>ExAllocatePool</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Hal</strong></p></td>
<td><p>硬件抽象层</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546596" data-raw-source="[&lt;strong&gt;HalGetAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546596)"><strong>HalGetAdapter</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Io</strong></p></td>
<td><p>I/O 管理器</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548257" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548257)"><strong>IoAllocateIrp</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ke</strong></p></td>
<td><p>内核核心</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"><strong>KeSetEvent</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Mm</strong></p></td>
<td><p>内存管理器</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556381" data-raw-source="[&lt;strong&gt;MmUnlockPages&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556381)"><strong>MmUnlockPages</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ob</strong></p></td>
<td><p>对象管理器</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff558678" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558678)"><strong>ObReferenceObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>采购订单</strong></p></td>
<td><p>电源管理器</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559765" data-raw-source="[&lt;strong&gt;PoSetPowerState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559765)"><strong>PoSetPowerState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Tm</strong></p></td>
<td><p>事务管理器</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564665" data-raw-source="[&lt;strong&gt;TmCommitTransaction&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564665)"><strong>TmCommitTransaction</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Nt</strong>和<strong>Zw</strong></p></td>
<td><p>本机系统服务</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157250" data-raw-source="[NtCreateFile](https://go.microsoft.com/fwlink/p/?linkid=157250)">NtCreateFile</a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff566424" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566424)"> <strong>zwcreatefile 转换</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




