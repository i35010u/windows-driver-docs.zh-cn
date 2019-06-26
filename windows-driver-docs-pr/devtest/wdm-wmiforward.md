---
title: WmiForward 规则 (wdm)
description: WmiForward 规则指定当需要转发时，该驱动程序必须转发 WMI 次要 Irp。
ms.assetid: c62f37d2-ebd5-4705-9590-d1bf17137802
ms.date: 05/21/2018
keywords:
- WmiForward 规则 (wdm)
topic_type:
- apiref
api_name:
- WmiForward
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1caaa93bfe843fa83df0d0f10a896201e58c149
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393101"
---
# <a name="wmiforward-rule-wdm"></a>WmiForward 规则 (wdm)


**WmiForward**规则指定驱动程序必须转发[ **WMI 次要 Irp** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)的转发操作。

具体而言，当驱动程序调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)的值*IrpDisposition*参数是**IrpForward**、驱动程序必须调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)或[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)将 IRP 转发从调度返回前例程。

此规则不适用于总线驱动程序。

一个*WMI 次要 IRP*是[ **IRP\_MJ\_系统\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control) WMI 次要函数代码的请求。

有关处理 WMI 次要 Irp 的详细信息，请参阅[ **WDM 驱动程序的 WMI 要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)， [**处理 WMI 请求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)， [**Windows Management Instrumentation 例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，和[ **WMI 库支持例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>WmiForward</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) See also
--------

[**用于 WDM 驱动程序的 WMI 要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)
[**处理 WMI 请求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)
[**WMI 库支持例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
 

 





