---
title: 'WmiComplete 规则 (wdm) '
description: WmiComplete 规则指定在处理 WMI 次要 IRP 时，驱动程序会在从 DispatchSystemControl 例程返回之前调用 IoCompleteRequest。
ms.assetid: 3908da96-beb1-4651-b41b-06f849b72000
ms.date: 05/21/2018
keywords:
- 'WmiComplete 规则 (wdm) '
topic_type:
- apiref
api_name:
- WmiComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b33b66138f93dcca7508a335e9d97387132aa3e
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381489"
---
# <a name="wmicomplete-rule-wdm"></a>WmiComplete 规则 (wdm) 


**WmiComplete**规则指定在处理[**WMI 次要 IRP**](../kernel/wmi-minor-irps.md)时，驱动程序会在从[**DispatchSystemControl**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回之前调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。

*Wmi 次要 IRP*是具有 WMI 次要函数代码的[**IRP \_ MJ \_ 系统 \_ 控制**](../kernel/irp-mj-system-control.md)请求。

有关处理 WMI 次要 Irp 的详细信息，请参阅 [**WDM 驱动程序的 Wmi 要求**](../kernel/wmi-requirements-for-wdm-drivers.md)、 [**处理 wmi 请求**](../kernel/handling-wmi-requests.md)、 [**Windows Management Instrumentation 例程**](/windows-hardware/drivers/ddi/index)和 [**WMI 库支持例程**](/windows-hardware/drivers/ddi/index)。

未注册为 WMI 数据提供程序的驱动程序必须将 WMI 请求转发到下一个较低版本的驱动程序。 若要验证此操作，请使用 [**WmiForward**](wdm-wmiforward.md) 规则。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WmiComplete</strong> 规则。</p>
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

[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 
[**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)另请参阅
--------

[**WmiForward**](wdm-wmiforward.md) 
[**WDM 驱动程序**](../kernel/wmi-requirements-for-wdm-drivers.md) 
 的 WMI 要求[**处理 WMI 请求**](../kernel/handling-wmi-requests.md) 
[**WMI 库支持例程**](/windows-hardware/drivers/ddi/index)
 

