---
title: 'IrqlDispatch 规则 (wdm) '
description: IrqlDispatch 规则指定，仅当驱动程序以 IRQL DISPATCH_LEVEL 执行时，才调用以下 DDIs。
ms.assetid: f72d4f27-b488-4d0a-97b7-9cb40f00e346
ms.date: 05/21/2018
keywords:
- 'IrqlDispatch 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlDispatch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b89151ad1f8b423e7e3f4f126a09a9664d69d161
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382054"
---
# <a name="irqldispatch-rule-wdm"></a>IrqlDispatch 规则 (wdm) 


**IrqlDispatch**规则指定，仅当驱动程序在 IRQL = 调度级别执行时，才调用以下 DDIs \_ 。

-   [**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)

-   [**FreeMapRegisters**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)

-   [**GetScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list)

-   [**IoAllocateAdapterChannel**](../kernel/mmcreatemdl.md)

-   [**IoAllocateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)

-   [**IoFreeController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)

-   [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)

-   [**KeAcquireSpinLockAtDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)

-   [**KeInsertByKeyDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue)

-   [**KeInsertDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue)

-   [**KeReleaseSpinLockFromDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)

-   [**KeRemoveByKeyDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovebykeydevicequeue)

-   [**KeRemoveDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue)

-   [**PutScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list)

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](../debugger/bug-check-0xa--irql-not-less-or-equal.md) ， [**bug 检查0xC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00020003) 


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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlDispatch</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**AllocateAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) 
[**AllocateCommonBuffer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer) 
[**BuildMdlFromScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pbuild_mdl_from_scatter_gather_list) 
[**BuildScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pbuild_scatter_gather_list) 
[**FlushAdapterBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) 
[**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) 
[**FreeCommonBuffer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_common_buffer) 
[**FreeMapRegisters**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers) 
[**GetDmaAlignment**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_alignment) 
[**GetScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list) 
[**IoAllocateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller) 
[**IoFreeController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller) 
[**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) 
[**IoWriteErrorLogEntry**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry) 
[**KeInsertByKeyDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue) 
[**KeInsertDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue) 
[**KeRemoveByKeyDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovebykeydevicequeue) 
[**KeRemoveDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue) 
[**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) 
[**PutDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_dma_adapter) 
[**PutScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list) 
[**ReadDmaCounter**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pread_dma_counter)另请参阅
--------

[**管理硬件优先级**](../kernel/managing-hardware-priorities.md) 
[**使用自旋锁时防止错误和死锁**](../kernel/preventing-errors-and-deadlocks-while-using-spin-locks.md)
 

