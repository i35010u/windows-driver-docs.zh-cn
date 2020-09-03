---
title: Irql 规则集 (Storport)
description: 使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。
ms.assetid: 3322200A-2073-4568-B1FC-481B216D8F61
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: e120b3bea09a3cdf3183bf542e7c395b8498c892
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383929"
---
# <a name="irql-rule-set-storport"></a>Irql 规则集 (Storport)


使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。

不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p><a href="storport-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](storport-irqldispatch.md)"><strong>IrqlDispatch</strong></a></p></td>
<td align="left"><p>此规则验证以下例程是否仅在 <strong>IRQL = DISPATCH_LEVEL</strong>调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](storport-irqlkereleasespinlock.md)"><strong>IrqlKeReleaseSpinLock</strong></a></p></td>
<td align="left"><p>此规则验证 <strong>KeReleaseSpinLock</strong> 在 <strong>IRQL = DISPATCH_LEVEL</strong> 上调用。 它还必须将 IRQL 设置为以前的 IRQL 级别。 通常，此调用之前会调用 <strong>KeAcquireSpinLock</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spchangeirql.md" data-raw-source="[&lt;strong&gt;SpChangeIrql&lt;/strong&gt;](storport-spchangeirql.md)"><strong>SpChangeIrql</strong></a></p></td>
<td align="left"><p>此规则验证 StorPort 回调例程是否返回的 IRQL 级别与调用它们的级别相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spirql.md" data-raw-source="[&lt;strong&gt;SpIrql&lt;/strong&gt;](storport-spirql.md)"><strong>SpIrql</strong></a></p></td>
<td align="left"><p>此规则验证例程 <strong>TdiRegisterPnPHandlers</strong> 和 <strong>TDIDEREGISTERPNPHANDLERS</strong> 仅在 IRQL 低于 <strong>DISPATCH_LEVEL</strong>的情况下调用。 但是，如果调用 <strong>ExFreeToNPagedLookasideList</strong> ，则规则通过。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportirql.md" data-raw-source="[&lt;strong&gt;StorPortIrql&lt;/strong&gt;](storport-storportirql.md)"><strong>StorPortIrql</strong></a></p></td>
<td align="left"><p><a href="storport-storportirql.md" data-raw-source="[&lt;strong&gt;StorPortIrql&lt;/strong&gt;](storport-storportirql.md)"><strong>StorPortIrql</strong></a>规则检查 StorPort 例程是否是以正确的 IRQL 级别调用的。</p></td>
</tr>
</tbody>
</table>

 

**选择 Irql 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **Irql**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请将 **sdv** 与 **/check** 选项一起指定。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

