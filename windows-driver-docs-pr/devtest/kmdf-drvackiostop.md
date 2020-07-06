---
title: DrvAckIoStop 规则（kmdf）
description: DrvAckIoStop 规则验证驱动程序是否能够识别出挂起的请求，同时驱动程序的电源管理队列正在关闭，驱动程序会相应地确认、完成或取消挂起的请求。
ms.assetid: 4C6F8919-C3DF-4DE2-94EF-45475CE9E0C0
ms.date: 05/21/2018
keywords:
- DrvAckIoStop 规则（kmdf）
topic_type:
- apiref
api_name:
- DrvAckIoStop
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: efa0fafdcd8af91bb2eff3fc54c4b5cfd94b9262
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967936"
---
# <a name="drvackiostop-rule-kmdf"></a>DrvAckIoStop 规则（kmdf）


**DrvAckIoStop**规则验证驱动程序是否能够识别出挂起的请求，同时驱动程序的电源管理队列正在关闭，驱动程序会相应地确认、完成或取消挂起的请求。 对于自托管 i/o 请求，驱动程序还应从其[*EvtDeviceSelfManagedIoSuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)函数正确处理这些请求。 关闭时无法处理这些请求的驱动程序会导致[**错误检查0x9F：驱动程序 \_ 电源 \_ 状态 \_ 故障**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure)。

在某些情况下，可能适合禁止显示此警告。 如果驱动程序没有保留请求，或未将其转发给其他驱动程序，并且如果驱动程序直接在队列的处理程序中完成请求，则可以使用** \_ \_ analysis \_ 假设**函数来禁止显示警告。 有关详细信息，请参阅[使用 \_ 分析 \_ 假设函数取消错误缺陷](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-the--analysis-assume-function-to-suppress-false-defects)和[**如何：通过使用 \_ \_ 分析 \_ 来指定其他代码信息**](https://docs.microsoft.com/visualstudio/code-quality/how-to-specify-additional-code-information-by-using-analysis-assume?view=vs-2015)。

**驱动程序模型： KMDF**

**找到了具有此规则的 bug 检查**： [ **bug 检查0x9F：驱动程序 \_ 电源 \_ 状态 \_ 故障**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure)


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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>DrvAckIoStop</strong>规则。</p>
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

[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) 
[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter) 
[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)
 

 





