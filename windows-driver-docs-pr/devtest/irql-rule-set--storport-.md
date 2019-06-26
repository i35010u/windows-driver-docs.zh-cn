---
title: Irql 规则集 (Storport)
description: 使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。
ms.assetid: 3322200A-2073-4568-B1FC-481B216D8F61
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 17d6c8f838e8662ed7963477468cad197072e0ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373669"
---
# <a name="irql-rule-set-storport"></a>Irql 规则集 (Storport)


使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。

未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。

## <a name="in-this-section"></a>本节内容


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
<td align="left"><p><a href="storport-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](storport-irqldispatch.md)"><strong>IrqlDispatch</strong></a></p></td>
<td align="left"><p>此规则验证，仅在调用以下例程<strong>IRQL = DISPATCH_LEVEL</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](storport-irqlkereleasespinlock.md)"><strong>IrqlKeReleaseSpinLock</strong></a></p></td>
<td align="left"><p>此规则验证<strong>KeReleaseSpinLock</strong>在调用<strong>IRQL = DISPATCH_LEVEL</strong>仅。 它还必须设置为以前的 IRQL 级别的 IRQL。 此调用通常会通过调用前面<strong>KeAcquireSpinLock</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spchangeirql.md" data-raw-source="[&lt;strong&gt;SpChangeIrql&lt;/strong&gt;](storport-spchangeirql.md)"><strong>SpChangeIrql</strong></a></p></td>
<td align="left"><p>此规则验证 StorPort 回调例程返回相同的 IRQL 与级别的调用它们的级别。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spirql.md" data-raw-source="[&lt;strong&gt;SpIrql&lt;/strong&gt;](storport-spirql.md)"><strong>SpIrql</strong></a></p></td>
<td align="left"><p>此规则验证例程<strong>TdiRegisterPnPHandlers</strong>并<strong>TdiDeregisterPnPHandlers</strong>仅在调用 IRQL 低于<strong>DISPATCH_LEVEL</strong>。 但是，如果<strong>ExFreeToNPagedLookasideList</strong>调用时，规则传递。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportirql.md" data-raw-source="[&lt;strong&gt;StorPortIrql&lt;/strong&gt;](storport-storportirql.md)"><strong>StorPortIrql</strong></a></p></td>
<td align="left"><p><a href="storport-storportirql.md" data-raw-source="[&lt;strong&gt;StorPortIrql&lt;/strong&gt;](storport-storportirql.md)"> <strong>StorPortIrql</strong> </a>规则检查，以正确的 IRQL 级别调用 StorPort 例程。</p></td>
</tr>
</tbody>
</table>

 

**若要选择的 Irql 规则设置**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**Irql**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Irql.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





