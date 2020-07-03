---
title: ForwardedAtBadIrqlAllocate 规则（wdm）
description: ForwardedAtBadIrqlAllocate 规则指定驱动程序应在 IRQL 调度级别调用 IoCallDriver 和 PoCallDriver \_ ，除非要转发的 irp 主要函数代码是以下 irp \_ mj \_ POWERIRP \_ mj \_ READIRP \_ mj \_ WRITEIRP mj \_ \_ DEVICE \_ CONTROLIRP \_ mj \_ INTERNAL \_ device \_ CONTROL。
ms.assetid: 74BB8358-AE25-4FF8-BBA7-BF108DC2946C
ms.date: 05/21/2018
keywords:
- ForwardedAtBadIrqlAllocate 规则（wdm）
topic_type:
- apiref
api_name:
- ForwardedAtBadIrqlAllocate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d679aab97936c40927199d28a16857c073bdf5d0
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916132"
---
# <a name="forwardedatbadirqlallocate-rule-wdm"></a>ForwardedAtBadIrqlAllocate 规则（wdm）


**ForwardedAtBadIrqlAllocate**规则指定驱动程序应在 IRQL 调度级别调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)和[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) &lt; \_ ，除非要转发的 IRP 主要函数代码是以下项之一：

-   [**IRP \_ MJ \_ POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)
-   [**IRP \_ MJ \_ 读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)
-   [**IRP \_ MJ \_ 写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)
-   [**IRP \_ MJ \_ 设备 \_ 控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)
-   [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>ForwardedAtBadIrqlAllocate</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





