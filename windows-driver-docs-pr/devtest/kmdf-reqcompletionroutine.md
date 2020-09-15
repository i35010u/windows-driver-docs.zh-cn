---
title: 'ReqCompletionRoutine 规则 (kmdf) '
description: ReqCompletionRoutine 规则指定在向 i/o 目标发送请求之前必须设置完成例程。
ms.assetid: 0ddf6980-0540-4224-9800-3cd534f03230
ms.date: 05/21/2018
keywords:
- 'ReqCompletionRoutine 规则 (kmdf) '
topic_type:
- apiref
api_name:
- ReqCompletionRoutine
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6479629f693cd87c4ef5c0218346d1a621f3254
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104064"
---
# <a name="reqcompletionroutine-rule-kmdf"></a>ReqCompletionRoutine 规则 (kmdf) 


**ReqCompletionRoutine**规则指定在向 i/o 目标发送请求之前必须设置完成例程。

如果请求不是同步发送的，或者不是以 "发送" 和 "忘记" 的形式发送的)  (，则该驱动程序应设置一个完成例程，以便在请求完成时，i/o 目标可以通知该驱动程序。 ** \_ \_ \_ \_ \_ \_ **

**驱动程序模型： KMDF**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>ReqCompletionRoutine</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 
[**WdfRequestSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)另请参阅
--------

[完成 I/o 请求](../wdf/completing-i-o-requests.md) 
[同步取消和完成代码](../wdf/synchronizing-cancel-and-completion-code.md) 
[**WDF \_请求 \_ 发送 \_ 选项 \_ 标志**](/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags) 
 [**WDF \_ 请求 \_ 发送 \_ 选项**](/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options)
