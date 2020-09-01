---
title: 使用代理连接跟踪
description: 使用代理连接跟踪
ms.assetid: 20A737D7-043D-4D05-A15D-85595E48521B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 011b227b008668962420affd49bb0e3c686cd040
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215773"
---
# <a name="using-proxied-connections-tracking"></a>使用代理连接跟踪


Windows 8 及更高版本的 Windows 支持代理连接跟踪。

此 WFP 功能有助于跟踪重定向 "记录" 从连接初始重定向到目标的最终连接的情况。 WFP 还允许标注驱动程序重定向连接。

### <a name="proxied-connections-tracking"></a>代理连接跟踪

由于存在多个代理 (例如，由不同的 Isv 开发) 由一方用来与最终目标通信的连接将被第二方重定向;而且，原始方可能再次重定向新连接。 如果没有连接跟踪，原始连接可能永远不会到达最终目标，因为它停滞在无限代理循环中。

向数据字段标识符添加支持连接跟踪的内容包括：

<a href="" id="fwps-field-xxx-ale-original-app-id"></a>FWPS \_ 字段 \_ Xxx \_ ALE \_ 原始 \_ 应用 \_ ID  
用于代理连接的原始应用程序的完整路径。 如果尚未对应用程序进行代理，则此路径等同于 xxx \_ ALE \_ 应用 \_ ID。

<a href="" id="fwps-field-xxx-package-id"></a>FWPS \_ 字段 \_ Xxx \_ 包 \_ ID  
包标识符是 (SID) 的安全标识符，用于标识关联的 AppContainer 进程。 有关 SID 结构的详细信息，请参阅 Microsoft Windows SDK 文档中 SID 结构的描述。

### <a name="redirecting-connections"></a>重定向连接

标注驱动程序调用 [**FwpsRedirectHandleCreate0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0) 函数来创建一个可用于重定向 TCP 连接的句柄。

本节包括下列主题：

使用重定向句柄

查询重定向状态

### <a name="using-a-redirection-handle"></a>使用重定向句柄

在 ALE 连接重定向标注可以将连接重定向到本地进程之前，必须使用 FwpsRedirectHandleCreate0 函数获取重定向句柄，并将该句柄置于 [**FWPS \_ connect \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0) 结构中。 标注会修改 ALE 连接重定向层的 classifyFn 中的结构。

FWPS \_ CONNECT \_ REQUEST0 结构包含以下重定向成员：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>localRedirectHandle</strong></p></td>
<td align="left"><p>标注驱动程序通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0" data-raw-source="[&lt;strong&gt;FwpsRedirectHandleCreate0&lt;/strong&gt;](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)"><strong>FwpsRedirectHandleCreate0</strong></a> 函数创建的重定向句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>localRedirectContext</strong></p></td>
<td align="left"><p>标注驱动程序上下文区域，标注驱动程序通过调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"><strong>ExAllocatePoolWithTag</strong></a> 函数进行分配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>localRedirectContextSize</strong></p></td>
<td align="left"><p>标注提供的上下文区域的大小（以字节为单位）。</p></td>
</tr>
</tbody>
</table>

 

使用重定向句柄完成标注驱动程序后，它必须调用 [**FwpsRedirectHandleDestroy0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandledestroy0) 函数以销毁句柄。

### <a name="querying-the-redirect-state"></a>查询重定向状态

标注驱动程序调用 [**FwpsQueryConnectionRedirectState0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0) 函数以获取连接的重定向状态。 [**FWPS \_ 连接 \_ 重定向 \_ 状态**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_connection_redirect_state_)枚举是对**FwpsQueryConnectionRedirectState0**函数的调用的返回类型。

如果重定向状态为 "FWPS \_ 连接 \_ 未 \_ 重定向"，则 ALE \_ 连接 \_ 重定向标注可以继续代理连接。

如果重定向状态是 FWPS \_ \_ 通过 SELF 重定向的连接 \_ \_ ，ALE \_ 连接 \_ 重定向标注应返回 .Fwp \_ 操作 \_ 允许/.fwp \_ 操作 \_ 继续。

如果重定向状态为 "FWPS \_ 连接被 \_ 其他重定向" \_ ，则 \_ ALE \_ 连接 \_ 重定向标注在不信任其他检查器的结果时，可以继续代理连接。

如果重定向状态是 \_ \_ 先前 \_ 通过 SELF 重定向的 FWPS 连接 \_ \_ ，则 ALE \_ 连接 \_ 重定向标注不得执行重定向，即使其他检查器的结果是不可接受的。 在这种情况下，它必须允许或阻止在 ALE \_ 身份验证 \_ 连接层)  (的连接。

 

