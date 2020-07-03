---
title: LowerDriverReturn 规则（wdm）
description: LowerDriverReturn 规则指定在使用 PoCallDriver 或 IoCallDriver 调用较低的驱动程序后，该驱动程序将从调用中保存返回状态，并将接收到的返回状态传递到调度例程。
ms.assetid: 0b437591-c613-481a-a4f9-36a5cc208cb0
ms.date: 05/21/2018
keywords:
- LowerDriverReturn 规则（wdm）
topic_type:
- apiref
api_name:
- LowerDriverReturn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 483172dd841b4abda0c4c823f5235dab84b20551
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916247"
---
# <a name="lowerdriverreturn-rule-wdm"></a>LowerDriverReturn 规则（wdm）


**LowerDriverReturn**规则指定在使用[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)或[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)调用较低的驱动程序后，该驱动程序将从调用中保存返回状态，并将接收到的返回状态传递到调度例程。

如果驱动程序调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)或[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，则不会应用这些条件。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>LowerDriverReturn</strong>规则。</p>
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

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 
[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 
[**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex) 
[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate) 
[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol) 
[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





