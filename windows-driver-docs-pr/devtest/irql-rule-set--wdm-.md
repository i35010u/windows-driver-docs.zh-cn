---
title: Irql rule set (WDM)
description: 使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。
ms.assetid: 40C17906-58D5-4023-A549-0164C3A92A06
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 71e8b5b305fa5b3ca3c53d52a72888aaa6358a78
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383927"
---
# <a name="irql-rule-set-wdm"></a>Irql rule set (WDM)


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
<td align="left"><p><a href="wdm-forwardedatbadirql.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrql&lt;/strong&gt;](wdm-forwardedatbadirql.md)"><strong>ForwardedAtBadIrql</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirql.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrql&lt;/strong&gt;](wdm-forwardedatbadirql.md)"><strong>ForwardedAtBadIrql</strong></a>规则指定在以下情况下，驱动程序应在 IRQL DISPATCH_LEVEL 调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a> &lt; ：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-forwardedatbadirqlallocate.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlAllocate&lt;/strong&gt;](wdm-forwardedatbadirqlallocate.md)"><strong>ForwardedAtBadIrqlAllocate</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlallocate.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlAllocate&lt;/strong&gt;](wdm-forwardedatbadirqlallocate.md)"><strong>ForwardedAtBadIrqlAllocate</strong></a>规则指定驱动程序应以 IRQL DISPATCH_LEVEL 调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a> &lt; ，除非要转发的 IRP 主要函数代码是以下项之一：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](../kernel/irp-mj-power.md)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](../kernel/irp-mj-read.md)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](../kernel/irp-mj-write.md)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](../kernel/irp-mj-device-control.md)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](../kernel/irp-mj-internal-device-control.md)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdasync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdAsync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdasync.md)"><strong>ForwardedAtBadIrqlFsdAsync</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdasync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdAsync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdasync.md)"><strong>ForwardedAtBadIrqlFsdAsync</strong></a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a> &lt; DISPATCH_LEVEL，除非要转发的 IRP 主要函数代码是以下项之一：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](../kernel/irp-mj-power.md)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](../kernel/irp-mj-read.md)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](../kernel/irp-mj-write.md)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](../kernel/irp-mj-device-control.md)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](../kernel/irp-mj-internal-device-control.md)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdsync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdSync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdsync.md)"><strong>ForwardedAtBadIrqlFsdSync</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdsync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdSync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdsync.md)"><strong>ForwardedAtBadIrqlFsdSync</strong></a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a> &lt; DISPATCH_LEVEL，除非要转发的 IRP 主要函数代码是以下项之一：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](../kernel/irp-mj-power.md)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](../kernel/irp-mj-read.md)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](../kernel/irp-mj-write.md)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](../kernel/irp-mj-device-control.md)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](../kernel/irp-mj-internal-device-control.md)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlapclte.md" data-raw-source="[&lt;strong&gt;IrqlApcLte&lt;/strong&gt;](wdm-irqlapclte.md)"><strong>IrqlApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlapclte.md" data-raw-source="[&lt;strong&gt;IrqlApcLte&lt;/strong&gt;](wdm-irqlapclte.md)"><strong>IrqlApcLte</strong></a>规则指定仅当驱动程序在 IRQL = APC_LEVEL 上执行时，驱动程序才调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obgetobjectsecurity" data-raw-source="[&lt;strong&gt;ObGetObjectSecurity&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-obgetobjectsecurity)"><strong>ObGetObjectSecurity</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreleaseobjectsecurity" data-raw-source="[&lt;strong&gt;ObReleaseObjectSecurity&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreleaseobjectsecurity)"><strong>ObReleaseObjectSecurity</strong></a> &lt; 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](wdm-irqldispatch.md)"><strong>IrqlDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](wdm-irqldispatch.md)"><strong>IrqlDispatch</strong></a>规则指定仅当驱动程序在 IRQL = DISPATCH_LEVEL 上执行时，才调用以下 DDIs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexallocatepool.md" data-raw-source="[&lt;strong&gt;IrqlExAllocatePool&lt;/strong&gt;](wdm-irqlexallocatepool.md)"><strong>IrqlExAllocatePool</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexallocatepool.md" data-raw-source="[&lt;strong&gt;IrqlExAllocatePool&lt;/strong&gt;](wdm-irqlexallocatepool.md)"><strong>IrqlExAllocatePool</strong></a>规则指定仅当驱动程序在 IRQL = DISPATCH_LEVEL 上执行时，驱动程序才调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"><strong>ExAllocatePoolWithTag</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTagPriority&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)"><strong>ExAllocatePoolWithTagPriority</strong></a> &lt; 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexapclte1.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte1&lt;/strong&gt;](wdm-irqlexapclte1.md)"><strong>IrqlExApcLte1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte1.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte1&lt;/strong&gt;](wdm-irqlexapclte1.md)"><strong>IrqlExApcLte1</strong></a>规则指定驱动程序仅调用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireFastMutex&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))"><strong>ExAcquireFastMutex</strong></a>和<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85)" data-raw-source="[&lt;strong&gt;ExTryToAcquireFastMutex&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))"><strong>ExTryToAcquireFastMutex</strong></a> ，而不是以 IRQL &lt; = APC_LEVEL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexapclte2.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte2&lt;/strong&gt;](wdm-irqlexapclte2.md)"><strong>IrqlExApcLte2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte2.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte2&lt;/strong&gt;](wdm-irqlexapclte2.md)"><strong>IrqlExApcLte2</strong></a>规则指定该驱动程序仅在 IRQL = APC_LEVEL 调用以下例程 &lt; 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexapclte3.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte3&lt;/strong&gt;](wdm-irqlexapclte3.md)"><strong>IrqlExApcLte3</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte3.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte3&lt;/strong&gt;](wdm-irqlexapclte3.md)"><strong>IrqlExApcLte3</strong></a>规则指定该驱动程序只调用 IRQL = APC_LEVEL 上的以下执行支持例程 &lt; 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexapclteinline.md" data-raw-source="[&lt;strong&gt;IrqlExApcLteInline&lt;/strong&gt;](wdm-irqlexapclteinline.md)"><strong>IrqlExApcLteInline</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclteinline.md" data-raw-source="[&lt;strong&gt;IrqlExApcLteInline&lt;/strong&gt;](wdm-irqlexapclteinline.md)"><strong>IrqlExApcLteInline</strong></a>规则指定仅在适当的 IRQL 级别调用 DDIs</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexfree1.md" data-raw-source="[&lt;strong&gt;IrqlExFree1&lt;/strong&gt;](wdm-irqlexfree1.md)"><strong>IrqlExFree1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree1.md" data-raw-source="[&lt;strong&gt;IrqlExFree1&lt;/strong&gt;](wdm-irqlexfree1.md)"><strong>IrqlExFree1</strong></a>规则指定以正确的 IRQL 调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>ExFreePool</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)"><strong>ExFreePoolWithTag</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexfree2.md" data-raw-source="[&lt;strong&gt;IrqlExFree2&lt;/strong&gt;](wdm-irqlexfree2.md)"><strong>IrqlExFree2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree2.md" data-raw-source="[&lt;strong&gt;IrqlExFree2&lt;/strong&gt;](wdm-irqlexfree2.md)"><strong>IrqlExFree2</strong></a>规则指定以正确的 IRQL 调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>ExFreePool</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)"><strong>ExFreePoolWithTag</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexfree3.md" data-raw-source="[&lt;strong&gt;IrqlExFree3&lt;/strong&gt;](wdm-irqlexfree3.md)"><strong>IrqlExFree3</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree3.md" data-raw-source="[&lt;strong&gt;IrqlExFree3&lt;/strong&gt;](wdm-irqlexfree3.md)"><strong>IrqlExFree3</strong></a>规则指定以正确的 IRQL 调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>ExFreePool</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)"><strong>ExFreePoolWithTag</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"><strong>IrqlExPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"><strong>IrqlExPassive</strong></a>规则指定驱动程序只调用以下执行程序支持例程： IRQL = PASSIVE_LEVEL：</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback" data-raw-source="[&lt;strong&gt;ExCreateCallback&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)"><strong>ExCreateCallback</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent" data-raw-source="[&lt;strong&gt;ExIsProcessorFeaturePresent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent)"><strong>ExIsProcessorFeaturePresent</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation" data-raw-source="[&lt;strong&gt;ExRaiseAccessViolation&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation)"><strong>ExRaiseAccessViolation</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment" data-raw-source="[&lt;strong&gt;ExRaiseDatatypeMisalignment&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment)"><strong>ExRaiseDatatypeMisalignment</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus" data-raw-source="[&lt;strong&gt;ExRaiseStatus&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)"><strong>ExRaiseStatus</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate" data-raw-source="[&lt;strong&gt;ExUuidCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate)"><strong>ExUuidCreate</strong></a></p></li>
</ul>
<p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"><strong>IrqlExPassive</strong></a>规则还指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus" data-raw-source="[&lt;strong&gt;ExRaiseStatus&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)"><strong>ExRaiseStatus</strong></a>的 IRQL &lt; = APC_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlioapclte.md" data-raw-source="[&lt;strong&gt;IrqlIoApcLte&lt;/strong&gt;](wdm-irqlioapclte.md)"><strong>IrqlIoApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlioapclte.md" data-raw-source="[&lt;strong&gt;IrqlIoApcLte&lt;/strong&gt;](wdm-irqlioapclte.md)"><strong>IrqlIoApcLte</strong></a>规则指定，仅当驱动程序在 IRQL = APC_LEVEL 上执行时，才调用以下 i/o 管理器例程 &lt; ：</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice" data-raw-source="[&lt;strong&gt;IoDeleteDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)"><strong>IoDeleteDevice</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetinitialstack" data-raw-source="[&lt;strong&gt;IoGetInitialStack&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetinitialstack)"><strong>IoGetInitialStack</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseharderror" data-raw-source="[&lt;strong&gt;IoRaiseHardError&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseharderror)"><strong>IoRaiseHardError</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseinformationalharderror" data-raw-source="[&lt;strong&gt;IoRaiseInformationalHardError&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseinformationalharderror)"><strong>IoRaiseInformationalHardError</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliodispatch.md" data-raw-source="[&lt;strong&gt;IrqlIoDispatch&lt;/strong&gt;](wdm-irqliodispatch.md)"><strong>IrqlIoDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliodispatch.md" data-raw-source="[&lt;strong&gt;IrqlIoDispatch&lt;/strong&gt;](wdm-irqliodispatch.md)"><strong>IrqlIoDispatch</strong></a>规则指定，仅当驱动程序在 IRQL &lt; = DISPATCH_LEVEL： <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetdevicetoverify" data-raw-source="[&lt;strong&gt;IoGetDeviceToVerify&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetdevicetoverify)"><strong>IoGetDeviceToVerify</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetdevicetoverify" data-raw-source="[&lt;strong&gt;IoSetDeviceToVerify&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetdevicetoverify)"><strong>IoSetDeviceToVerify</strong></a>的情况下执行时，才调用以下 i/o 管理器例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive1.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive1&lt;/strong&gt;](wdm-irqliopassive1.md)"><strong>IrqlIoPassive1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive1.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive1&lt;/strong&gt;](wdm-irqliopassive1.md)"><strong>IrqlIoPassive1</strong></a>规则指定，仅当驱动程序在 IRQL = PASSIVE_LEVEL 上执行时，才调用以下例程：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliopassive2.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive2&lt;/strong&gt;](wdm-irqliopassive2.md)"><strong>IrqlIoPassive2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive2.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive2&lt;/strong&gt;](wdm-irqliopassive2.md)"><strong>IrqlIoPassive2</strong></a>规则指定驱动程序只调用以下 I/o 管理器例程： IRQL = PASSIVE_LEVEL：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive3.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive3&lt;/strong&gt;](wdm-irqliopassive3.md)"><strong>IrqlIoPassive3</strong></a></p></td>
<td align="left"><p>IrqlIoPassive3 规则指定，仅当驱动程序在 IRQL = PASSIVE_LEVEL 上执行时，才调用以下例程：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliopassive4.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive4&lt;/strong&gt;](wdm-irqliopassive4.md)"><strong>IrqlIoPassive4</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive4.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive4&lt;/strong&gt;](wdm-irqliopassive4.md)"><strong>IrqlIoPassive4</strong></a>规则指定，仅当驱动程序在 IRQL = PASSIVE_LEVEL 上执行时，才调用以下例程：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive5.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive5&lt;/strong&gt;](wdm-irqliopassive5.md)"><strong>IrqlIoPassive5</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive5.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive5&lt;/strong&gt;](wdm-irqliopassive5.md)"><strong>IrqlIoPassive5</strong></a>规则指定，仅当驱动程序在 IRQL = PASSIVE_LEVEL 上执行时，才调用特定的 I/o 管理器例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliortlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlIoRtlZwPassive&lt;/strong&gt;](wdm-irqliortlzwpassive.md)"><strong>IrqlIoRtlZwPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliortlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlIoRtlZwPassive&lt;/strong&gt;](wdm-irqliortlzwpassive.md)"><strong>IrqlIoRtlZwPassive</strong></a>规则指定，仅当驱动程序在 IRQL = PASSIVE_LEVEL 上执行时，才调用特定的 I/o 管理器例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkeapclte1.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte1&lt;/strong&gt;](wdm-irqlkeapclte1.md)"><strong>IrqlKeApcLte1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeapclte1.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte1&lt;/strong&gt;](wdm-irqlkeapclte1.md)"><strong>IrqlKeApcLte1</strong></a>规则指定，仅当驱动程序在 IRQL = APC_LEVEL 上执行时，才调用以下内核例程 &lt; ：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkeapclte2.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte2&lt;/strong&gt;](wdm-irqlkeapclte2.md)"><strong>IrqlKeApcLte2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeapclte2.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte2&lt;/strong&gt;](wdm-irqlkeapclte2.md)"><strong>IrqlKeApcLte2</strong></a>规则指定，仅当驱动程序在 IRQL = APC_LEVEL 上执行时，才调用以下内核例程 &lt; ：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkedispatchlte.md" data-raw-source="[&lt;strong&gt;IrqlKeDispatchLte&lt;/strong&gt;](wdm-irqlkedispatchlte.md)"><strong>IrqlKeDispatchLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkedispatchlte.md" data-raw-source="[&lt;strong&gt;IrqlKeDispatchLte&lt;/strong&gt;](wdm-irqlkedispatchlte.md)"><strong>IrqlKeDispatchLte</strong></a>规则指定，仅当驱动程序在 IRQL = DISPATCH_LEVEL 上执行时，才调用以下内核例程 &lt; ：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkeraiselower.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower&lt;/strong&gt;](wdm-irqlkeraiselower.md)"><strong>IrqlKeRaiseLower</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeraiselower" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower&lt;/strong&gt;](./wdm-irqlkeraiselower.md)"><strong>IrqlKeRaiseLower</strong></a>规则指定驱动程序在引发和降低 IRQL 时执行以下操作：</p>
当驱动程序调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql" data-raw-source="[&lt;strong&gt;KeRaiseIrql&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)"><strong>KeRaiseIrql</strong></a>时，它将在小于或等于 <em>NewIrql</em> 参数值的 IRQL 下执行。<br />
驱动程序仅在调用<strong>KeRaiseIrql</strong>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel" data-raw-source="[&lt;strong&gt;KeRaiseIrqlToDpcLevel&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)"><strong>KeRaiseIrqlToDpcLevel</strong></a>后调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql" data-raw-source="[&lt;strong&gt;KeLowerIrql&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)"><strong>KeLowerIrql</strong></a> 。<br />
</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkeraiselower2.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower2&lt;/strong&gt;](wdm-irqlkeraiselower2.md)"><strong>IrqlKeRaiseLower2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeraiselower2.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower2&lt;/strong&gt;](wdm-irqlkeraiselower2.md)"><strong>IrqlKeRaiseLower2</strong></a>规则指定驱动程序使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql" data-raw-source="[&lt;strong&gt;KeLowerIrql&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)"><strong>KeLowerIrql</strong></a>来还原前面调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql" data-raw-source="[&lt;strong&gt;KeRaiseIrql&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)"><strong>KeRaiseIrql</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel" data-raw-source="[&lt;strong&gt;KeRaiseIrqlToDpcLevel&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)"><strong>KeRaiseIrqlToDpcLevel</strong></a>引发的原始 IRQL。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](wdm-irqlkereleasespinlock.md)"><strong>IrqlKeReleaseSpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](wdm-irqlkereleasespinlock.md)"><strong>IrqlKeReleaseSpinLock</strong></a>规则指定，仅当驱动程序在 IRQL = DISPATCH_LEVEL 上执行时，才调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkesetevent.md" data-raw-source="[&lt;strong&gt;IrqlKeSetEvent&lt;/strong&gt;](wdm-irqlkesetevent.md)"><strong>IrqlKeSetEvent</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkesetevent.md" data-raw-source="[&lt;strong&gt;IrqlKeSetEvent&lt;/strong&gt;](wdm-irqlkesetevent.md)"><strong>IrqlKeSetEvent</strong></a>规则指定， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> &lt; 当<em>Wait</em>设置为<strong>FALSE</strong>时，KeSetEvent 例程仅在 irql = DISPATCH_LEVEL 调用，而 &lt; 当<em>wait</em>设置为<strong>TRUE</strong>时，则在 irql = APC_LEVEL。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkewaitformutexobject.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMutexObject&lt;/strong&gt;](wdm-irqlkewaitformutexobject.md)"><strong>IrqlKeWaitForMutexObject</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkewaitformutexobject.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMutexObject&lt;/strong&gt;](wdm-irqlkewaitformutexobject.md)"><strong>IrqlKeWaitForMutexObject</strong></a>规则根据<em>Timeout</em>参数的值，指定要在适当 IRQL 处调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553344" data-raw-source="[&lt;strong&gt;KeWaitForMutexObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553344)"><strong>KeWaitForMutexObject</strong></a>例程的驱动程序：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkewaitformultipleobjects.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMultipleObjects&lt;/strong&gt;](wdm-irqlkewaitformultipleobjects.md)"><strong>IrqlKeWaitForMultipleObjects</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkewaitformultipleobjects.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMultipleObjects&lt;/strong&gt;](wdm-irqlkewaitformultipleobjects.md)"><strong>IrqlKeWaitForMultipleObjects</strong></a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)"><strong>KeWaitForMultipleObjects</strong></a>例程的调用方必须基于<em>超时</em>参数在适当的 IRQL 上运行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlmmapclte.md" data-raw-source="[&lt;strong&gt;IrqlMmApcLte&lt;/strong&gt;](wdm-irqlmmapclte.md)"><strong>IrqlMmApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlmmapclte.md" data-raw-source="[&lt;strong&gt;IrqlMmApcLte&lt;/strong&gt;](wdm-irqlmmapclte.md)"><strong>IrqlMmApcLte</strong></a>规则指定，仅当驱动程序在 IRQL = APC_LEVEL 上执行时，才调用以下内存管理器例程 &lt; ：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlmmdispatch.md" data-raw-source="[&lt;strong&gt;IrqlMmDispatch&lt;/strong&gt;](wdm-irqlmmdispatch.md)"><strong>IrqlMmDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlmmdispatch.md" data-raw-source="[&lt;strong&gt;IrqlMmDispatch&lt;/strong&gt;](wdm-irqlmmdispatch.md)"><strong>IrqlMmDispatch</strong></a>规则指定，仅当驱动程序在<strong>IRQL &lt; = DISPATCH_LEVEL</strong>上执行时，才调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory" data-raw-source="[&lt;strong&gt;MmFreeContiguousMemory&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory)"><strong>MmFreeContiguousMemory</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlntifsapcpassive.md" data-raw-source="[&lt;strong&gt;IrqlNtifsApcPassive&lt;/strong&gt;](wdm-irqlntifsapcpassive.md)"><strong>IrqlNtifsApcPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlntifsapcpassive.md" data-raw-source="[&lt;strong&gt;IrqlNtifsApcPassive&lt;/strong&gt;](wdm-irqlntifsapcpassive.md)"><strong>IIrqlNtifsApcPassive</strong></a>规则指定，仅当该驱动程序以 irql = PASSIVE_LEVEL 或 irql 运行时，才调用该规则中列出的 DDIs <= APC_LEVEL.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlobpassive.md" data-raw-source="[&lt;strong&gt;IrqlObPassive&lt;/strong&gt;](wdm-irqlobpassive.md)"><strong>IrqlObPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlobpassive.md" data-raw-source="[&lt;strong&gt;IrqlObPassive&lt;/strong&gt;](wdm-irqlobpassive.md)"><strong>IrqlObPassive</strong></a>规则指定，仅当驱动程序在 IRQL = PASSIVE_LEVEL 上执行时，才调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>ObReferenceObjectByHandle</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlpspassive.md" data-raw-source="[&lt;strong&gt;IrqlPsPassive&lt;/strong&gt;](wdm-irqlpspassive.md)"><strong>IrqlPsPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlpspassive.md" data-raw-source="[&lt;strong&gt;IrqlPsPassive&lt;/strong&gt;](wdm-irqlpspassive.md)"><strong>IrqlPsPassive</strong></a>规则指定仅当驱动程序在 IRQL = PASSIVE_LEVEL 上执行时，才调用以下<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[&lt;strong&gt;Process Structure routines&lt;/strong&gt;](/windows-hardware/drivers/ddi/index)"><strong>进程结构例程</strong></a>：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlreturn.md" data-raw-source="[&lt;strong&gt;IrqlReturn&lt;/strong&gt;](wdm-irqlreturn.md)"><strong>IrqlReturn</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlreturn.md" data-raw-source="[&lt;strong&gt;IrqlReturn&lt;/strong&gt;](wdm-irqlreturn.md)"><strong>IrqlReturn</strong></a>规则指定驱动程序的调度例程在调用时返回的 IRQL 相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlrtlpassive.md" data-raw-source="[&lt;strong&gt;IrqlRtlPassive&lt;/strong&gt;](wdm-irqlrtlpassive.md)"><strong>IrqlRtlPassive</strong></a></p></td>
<td align="left"><p>IrqlRtlPassive 规则指定，仅当驱动程序在 IRQL = PASSIVE_LEVEL 上执行时，才调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue" data-raw-source="[&lt;strong&gt;RtlDeleteRegistryValue&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue)"><strong>RtlDeleteRegistryValue</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlZwPassive&lt;/strong&gt;](wdm-irqlzwpassive.md)"><strong>IrqlZwPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlZwPassive&lt;/strong&gt;](wdm-irqlzwpassive.md)"><strong>IrqlZwPassive</strong></a>规则指定，仅当驱动程序在 IRQL = PASSIVE_LEVEL 上执行时，才调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)"><strong>ZwClose</strong></a> 。</p></td>
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

 

