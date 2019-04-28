---
title: MdlAfterReqCompletedIoctl 规则 (kmdf)
description: MdlAfterReqCompletedIoctl 规则指定，在 EvtIoDeviceControl 回调函数的内部内存描述符列表 (MDL) 后，无法访问已完成的 I/O 请求。
ms.assetid: ce82cca4-f0e3-4e84-8599-4094fa1ed4c2
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedIoctl 规则 (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedIoctl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17d4a708d3c99d12be0d7dd79415235cd60d0f2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350377"
---
# <a name="mdlafterreqcompletedioctl-rule-kmdf"></a>MdlAfterReqCompletedIoctl 规则 (kmdf)


**MdlAfterReqCompletedIoctl**规则指定内[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)回调函数不能后访问内存描述符列表 (MDL)I/O 请求完成。

中的驱动程序[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)回调函数，通过调用检索到 MDL [ **WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016)或[ **WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)方法不能访问之后调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)， [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，或[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)上I/O 请求。

此规则在以下 MDL 访问函数所示：

[**WDF\_内存\_描述符\_INIT\_MDL**](https://msdn.microsoft.com/library/windows/hardware/ff552396)
[**MmGetMdlByteCount** ](https://msdn.microsoft.com/library/windows/hardware/ff554530) 
[ **MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)
[**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539) 
 [**IoBuildPartialMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548324) （第一个和第二个参数） [ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041) 
 [ **MmGetMdlPfnArray**](https://msdn.microsoft.com/library/windows/hardware/ff554537)
[**MmGetMdlByteOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff554533) 
 [ **MmPrepareMdlForReuse**](https://msdn.microsoft.com/library/windows/hardware/ff554660)
[**WdfDmaTransactionInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff547099)

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MdlAfterReqCompletedIoctl</strong>规则。</p>
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

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016) 
 [ **WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021)








