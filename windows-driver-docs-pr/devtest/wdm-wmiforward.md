---
title: 'WmiForward 规则 (wdm) '
description: WmiForward 规则指定当需要转发时，驱动程序必须转发 WMI 次要 Irp。
ms.assetid: c62f37d2-ebd5-4705-9590-d1bf17137802
ms.date: 05/21/2018
keywords:
- 'WmiForward 规则 (wdm) '
topic_type:
- apiref
api_name:
- WmiForward
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5eedbe2e6c6798ea3b584b8ffe02bff815e4b006
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381487"
---
# <a name="wmiforward-rule-wdm"></a>WmiForward 规则 (wdm) 


**WmiForward**规则指定当需要转发时，驱动程序必须转发[**WMI 次要 irp**](../kernel/wmi-minor-irps.md) 。

具体而言，当驱动程序调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 并且 *IrpDisposition* 参数的值为 **IrpForward**时，驱动程序必须调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 或 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) ，以便在从调度例程返回之前转发 IRP。

此规则不适用于总线驱动程序。

*Wmi 次要 IRP*是具有 WMI 次要函数代码的[**IRP \_ MJ \_ 系统 \_ 控制**](../kernel/irp-mj-system-control.md)请求。

有关处理 WMI 次要 Irp 的详细信息，请参阅 [**WDM 驱动程序的 Wmi 要求**](../kernel/wmi-requirements-for-wdm-drivers.md)、 [**处理 wmi 请求**](../kernel/handling-wmi-requests.md)、 [**Windows Management Instrumentation 例程**](/windows-hardware/drivers/ddi/index)和 [**WMI 库支持例程**](/windows-hardware/drivers/ddi/index)。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WmiForward</strong> 规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 
[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)另请参阅
--------

[**WDM 驱动程序**](../kernel/wmi-requirements-for-wdm-drivers.md) 
 的 WMI 要求[**处理 WMI 请求**](../kernel/handling-wmi-requests.md) 
[**WMI 库支持例程**](/windows-hardware/drivers/ddi/index)
 

