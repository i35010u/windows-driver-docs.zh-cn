---
title: Bug 检查 0x112 MSRPC_STATE_VIOLATION
description: MSRPC_STATE_VIOLATION bug 检查的值为0x00000112。 这表明 Msrpc.sys 驱动程序已启动 bug 检查。
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
ms.openlocfilehash: c80d2ec436ca76459e58601dc796a27194ea4a9f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823521"
---
# <a name="bug-check-0x112-msrpc_state_violation"></a>Bug 检查0x112： MSRPC \_ 状态 \_ 冲突


MSRPC \_ 状态 \_ 冲突 bug 检查的值为0x00000112。 这表明 Msrpc.sys 驱动程序已启动 bug 检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="msrpc_state_violation-parameters"></a>MSRPC \_ 状态 \_ 冲突参数


参数1和2是相关的唯一参数。 参数1指示状态冲突类型;参数2的值由参数1的值确定。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>异常代码</p></td>
<td align="left"><p>调用方继续出现无法继续操作的异常。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>错误</p></td>
<td align="left"><p> (ALPC) 的高级本地过程调用返回了无效错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>服务器会话</p></td>
<td align="left"><p>调用方在仍在使用时 (MSRPC) 驱动程序的情况下卸载了 Microsoft 远程过程调用。 打开的绑定句柄可能仍然存在。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04 和</p>
<p>0x05</p></td>
<td align="left"><p>服务器会话</p></td>
<td align="left"><p>从 ALPC 接收到无效的关闭命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>绑定句柄</p></td>
<td align="left"><p>尝试将远程过程调用绑定 (RPC) 第二次处理。</p></td>
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
<td align="left"><p>尝试在已绑定的绑定句柄上设置选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>Call 对象</p></td>
<td align="left"><p>尝试取消无效的异步远程过程调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>Call 对象</p></td>
<td align="left"><p>尝试在非预期的异步管道调用上推送。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C 和</p>
<p>0x0E</p></td>
<td align="left"><p>管道对象</p></td>
<td align="left"><p>尝试在异步管道上推送，无需等待通知。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>管道对象</p></td>
<td align="left"><p>再次尝试同步终止管道。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>最接近错误的对象</p></td>
<td align="left"><p>发生 RPC 内部错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>按不能由 RPC 强制执行的顺序发出了两个 causally 顺序调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>Call 对象</p></td>
<td align="left"><p>服务器管理器例程在完成调用之前未取消订阅通知。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x18</p></td>
<td align="left"><p>异步句柄</p></td>
<td align="left"><p>发生异步句柄上的无效操作。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误检查的最常见原因是 Msrpc.sys 驱动程序的调用方违反了此类调用的状态语义。

 

 




