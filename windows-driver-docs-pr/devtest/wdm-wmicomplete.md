---
title: WmiComplete 规则（wdm）
description: WmiComplete 规则指定在处理 WMI 次要 IRP 时，驱动程序会在从 DispatchSystemControl 例程返回之前调用 IoCompleteRequest。
ms.assetid: 3908da96-beb1-4651-b41b-06f849b72000
ms.date: 05/21/2018
keywords:
- WmiComplete 规则（wdm）
topic_type:
- apiref
api_name:
- WmiComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1284d546a4cea03eee9efef01e7458c11dce2097
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839092"
---
# <a name="wmicomplete-rule-wdm"></a>WmiComplete 规则（wdm）


**WmiComplete**规则指定在处理[**WMI 次要 IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)时，驱动程序会在从[**DispatchSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回之前调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。

*Wmi 次要 IRP*是一种[**IRP\_MJ\_系统\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)使用 WMI 次要函数代码的控制请求。

有关处理 WMI 次要 Irp 的详细信息，请参阅[**WDM 驱动程序的 Wmi 要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)、[**处理 wmi 请求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)、 [**Windows Management Instrumentation 例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)和[**WMI 库支持例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

未注册为 WMI 数据提供程序的驱动程序必须将 WMI 请求转发到下一个较低版本的驱动程序。 若要验证此操作，请使用[**WmiForward**](wdm-wmiforward.md)规则。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>WmiComplete</strong>规则。</p>
使用以下步骤来分析你的代码：
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

[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)
[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)另请参阅
--------

[**WmiForward**](wdm-wmiforward.md)
[**针对 WDM 驱动程序的 Wmi 要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)
处理 wmi[**库支持例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
wmi[**请求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)
 

 





