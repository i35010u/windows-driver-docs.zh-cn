---
title: MdlAfterReqCompletedReadA rule (kmdf)
description: MdlAfterReqCompletedReadA 规则指定，EvtIoRead 回调函数内检索到的内存描述符列表 (MDL) 对象后，无法访问已完成的 I/O 请求。
ms.assetid: 3e7c40a0-882e-45eb-8cf1-bee1096379ad
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedReadA rule (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedReadA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 293624ab43a47f8bc0a936bfe67cf637d850970d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350376"
---
# <a name="mdlafterreqcompletedreada-rule-kmdf"></a>MdlAfterReqCompletedReadA rule (kmdf)


**MdlAfterReqCompletedReadA**规则指定内[ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)回调函数不能为检索到的内存描述符列表 (MDL) 对象I/O 请求完成后，访问。

中的驱动程序*EvtIoRead*回调函数，通过调用检索到的请求缓冲区[ **WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)方法不能为在调用后访问[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)， [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，或[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 请求。

此规则会考虑以下函数：

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MdlAfterReqCompletedReadA</strong>规则。</p>
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

[**WDF\_内存\_描述符\_INIT\_MDL**](https://msdn.microsoft.com/library/windows/hardware/ff552396)
[**WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)
 [ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948)
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveOutputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550021)
 [ **IoBuildPartialMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548324)
[**KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041) 
 [**MmGetMdlByteCount**](https://msdn.microsoft.com/library/windows/hardware/ff554530)
[**MmGetMdlByteOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff554533) 
 [ **MmGetMdlPfnArray**](https://msdn.microsoft.com/library/windows/hardware/ff554537)
[**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539) 
 [ **MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)
[**MmPrepareMdlForReuse**](https://msdn.microsoft.com/library/windows/hardware/ff554660)








