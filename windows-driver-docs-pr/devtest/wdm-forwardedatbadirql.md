---
title: 'ForwardedAtBadIrql 规则 (wdm) '
ms.assetid: d2d91fb9-330b-420b-8409-509cfb47fe07
ms.date: 05/21/2018
description: '了解详细信息： ForwardedAtBadIrql 规则 (wdm) '
keywords:
- 'ForwardedAtBadIrql 规则 (wdm) '
topic_type:
- apiref
api_name:
- ForwardedAtBadIrql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6acf43a1a7c501a061120f1b2a1b8df210864836
ms.sourcegitcommit: f47c072e88dce59daba1231027b60eb56bd2cde9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92689408"
---
# <a name="forwardedatbadirql-rule-wdm"></a>ForwardedAtBadIrql 规则 (wdm) 


**ForwardedAtBadIrql** 规则指定， [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) &lt; \_ 除非要转发的 IRP 主要函数代码是以下内容之一，否则，驱动程序应以 IRQL 调度级别调用 IoCallDriver 和 PoCallDriver：

-   [**IRP \_ MJ \_ POWER**](../kernel/irp-mj-power.md)

-   [**IRP \_ MJ \_ 读取**](../kernel/irp-mj-read.md)

-   [**IRP \_ MJ \_ 写入**](../kernel/irp-mj-write.md)

-   [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md)

-   [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>ForwardedAtBadIrql</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[ **PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
