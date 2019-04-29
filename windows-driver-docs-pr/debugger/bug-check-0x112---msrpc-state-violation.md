---
title: Bug 检查 0x112 MSRPC_STATE_VIOLATION
description: MSRPC_STATE_VIOLATION bug 检查具有 0x00000112 值。 这表示 Msrpc.sys 驱动程序已启动的 bug 检查。
ms.assetid: b7cd531d-518e-4d11-8edb-d52dbbe51043
keywords:
- Bug 检查 0x112 MSRPC_STATE_VIOLATION
- MSRPC_STATE_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MSRPC_STATE_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9419d102cfafa89ffd3546b35e55d47c2d9829dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358186"
---
# <a name="bug-check-0x112-msrpcstateviolation"></a>Bug 检查 0x112：MSRPC\_状态\_冲突


MSRPC\_状态\_冲突错误检查的值为 0x00000112。 这表示 Msrpc.sys 驱动程序已启动的 bug 检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="msrpcstateviolation-parameters"></a>MSRPC\_状态\_冲突参数


参数 1 和 2 是感兴趣的唯一参数。 参数 1 指示状态冲突类型;参数 2 的值由参数 1 的值确定。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>异常代码</p></td>
<td align="left"><p>非持续性异常已由调用方继续运行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p>在高级本地过程调用 (ALPC) 返回了无效的错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>连接到服务器的会话</p></td>
<td align="left"><p>仍在使用时，调用方将卸载 Microsoft 远程过程调用 (MSRPC) 驱动程序。 很可能，仍将打开绑定句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04 和</p>
<p>0x05</p></td>
<td align="left"><p>连接到服务器的会话</p></td>
<td align="left"><p>从 ALPC 收到无效的关闭命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>绑定句柄</p></td>
<td align="left"><p>尝试将远程过程调用 (RPC) 句柄绑定第二次。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>绑定句柄</p></td>
<td align="left"><p>尝试对未绑定的绑定句柄执行操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>绑定句柄</p></td>
<td align="left"><p>尝试在已绑定的绑定句柄上设置安全信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>绑定句柄</p></td>
<td align="left"><p>尝试设置已绑定的绑定句柄上的选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>调用对象</p></td>
<td align="left"><p>尝试取消无效异步远程过程调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>调用对象</p></td>
<td align="left"><p>尝试时不应在异步管道调用推送。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C 和</p>
<p>0x0E</p></td>
<td align="left"><p>管道对象</p></td>
<td align="left"><p>尝试异步管道上推送而无需等待通知。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>管道对象</p></td>
<td align="left"><p>尝试以同步方式终止管道第二次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>最接近于错误对象</p></td>
<td align="left"><p>出现 RPC 内部错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>不能强制实施通过 RPC 的顺序发出两个 causally 有序的调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>调用对象</p></td>
<td align="left"><p>服务器管理器例程不未取消订阅通知前完成调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x18</p></td>
<td align="left"><p>异步句柄</p></td>
<td align="left"><p>无效操作异步句柄上的发生。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查的最常见原因是 Msrpc.sys 驱动程序的调用方违反了此类调用的状态语义。

 

 




