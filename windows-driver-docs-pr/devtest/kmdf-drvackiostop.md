---
title: DrvAckIoStop 规则 (kmdf)
description: DrvAckIoStop 规则验证该驱动程序挂起的请求，注意其电源管理队列是获取关机和驱动程序确认之后，完成后，或取消挂起的请求时相应地。
ms.assetid: 4C6F8919-C3DF-4DE2-94EF-45475CE9E0C0
ms.date: 05/21/2018
keywords:
- DrvAckIoStop 规则 (kmdf)
topic_type:
- apiref
api_name:
- DrvAckIoStop
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d199d9e30953ff276e9c6ebfc84cd86a14e43def
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350431"
---
# <a name="drvackiostop-rule-kmdf"></a>DrvAckIoStop 规则 (kmdf)


**DrvAckIoStop**规则验证该驱动程序是注意挂起的请求，而其电源管理队列即将关闭的该驱动程序确认、 完成后，或相应地取消挂起的请求。 对于自托管 I/O 请求，该驱动程序应也可以正确处理这些请求从其[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)函数。 无法在电源关闭过程中处理这些请求的驱动程序会导致[ **Bug 检查 0x9F:驱动程序\_电源\_状态\_失败**](https://msdn.microsoft.com/library/windows/hardware/ff559329)。

在某些情况下可能会相应地禁止显示此警告。 如果该驱动程序不保持请求，或不将它们转发到其他驱动程序，并且如果该驱动程序完成后直接在队列的处理程序中的请求，则可以使用 **\_\_分析\_假定**函数来禁止显示警告。 有关详细信息，请参阅[Using \_analysis\_假定函数禁止显示 False 缺陷](https://msdn.microsoft.com/library/windows/hardware/ff556059)和[**如何：指定使用的其他代码信息\_ \_analysis\_假定**](https://msdn.microsoft.com/library/windows/hardware/ms404702)。

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

|                                   |                                                                                                          |
|-----------------------------------|----------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0x9F:DRIVER\_POWER\_STATE\_FAILURE**](https://msdn.microsoft.com/library/windows/hardware/ff559329) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>DrvAckIoStop</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546135)
[**WdfFdoInitSetFilter**](https://msdn.microsoft.com/library/windows/hardware/ff547273)
[**WdfIoQueueCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547401)
 

 





