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
ms.openlocfilehash: 05c894d9023a043b4da6acd08bba4f09e8f53a77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840232"
---
# <a name="drvackiostop-rule-kmdf"></a>DrvAckIoStop 规则（kmdf）


**DrvAckIoStop**规则验证驱动程序是否能够识别出挂起的请求，同时驱动程序的电源管理队列正在关闭，驱动程序会相应地确认、完成或取消挂起的请求。 对于自托管 i/o 请求，驱动程序还应从其[*EvtDeviceSelfManagedIoSuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)函数正确处理这些请求。 关闭时无法处理这些请求的驱动程序会导致[**错误检查0x9F：驱动程序\_电源\_状态\_故障**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure)。

在某些情况下，可能适合禁止显示此警告。 如果驱动程序没有保留请求，或者不将其转发给其他驱动程序，并且如果驱动程序直接在队列的处理程序中完成请求，则可以使用 **\_\_分析\_假设**函数禁止显示出现. 有关详细信息，请参阅[使用 \_分析\_假设函数禁止显示错误](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-the--analysis-assume-function-to-suppress-false-defects)，以及[**如何：通过使用 \_\_分析\_假设来指定其他代码信息**](https://docs.microsoft.com/visualstudio/code-quality/how-to-specify-additional-code-information-by-using-analysis-assume?view=vs-2015)。

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

|                                   |                                                                                                          |
|-----------------------------------|----------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查0x9F：驱动程序\_电源\_状态\_故障**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure) |

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

<a name="applies-to"></a>适用范围
----------

[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)
[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)
[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)
 

 





