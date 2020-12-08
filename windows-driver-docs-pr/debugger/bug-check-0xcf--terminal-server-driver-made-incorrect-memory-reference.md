---
title: Bug 检查 0xCF TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
description: TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE bug 检查的值为0x000000CF。 这表明驱动程序未正确地移植到终端服务器。
keywords:
- Bug 检查 0xCF TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
- TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80958514ffa2b9a3bc00b12a3e41968601929fcf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825199"
---
# <a name="bug-check-0xcf-terminal_server_driver_made_incorrect_memory_reference"></a>Bug 检查0xCF：终端 \_ 服务器 \_ 驱动程序 \_ 进行了 \_ 错误的 \_ 内存 \_ 引用


终端 \_ 服务器 \_ 驱动程序 \_ 进行 \_ 错误 \_ \_ 的内存引用 bug 检查的值为0x000000CF。 这表明驱动程序未正确地移植到终端服务器。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="terminal_server_driver_made_incorrect_memory_reference-parameters"></a>终端 \_ 服务器 \_ 驱动程序 \_ 进行了 \_ 错误的 \_ 内存 \_ 引用参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>引用的内存地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0：</strong> 读取</p>
<p><strong>1：</strong> 写入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>引用内存的地址（如果已知）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

如果能够识别出导致错误的驱动程序，则其名称将打印在蓝屏上，并存储在内存中的 (PUNICODE\_STRING) KiBugCheckDriver  位置。

<a name="cause"></a>原因
-----

驱动程序正在从系统进程上下文中引用会话空间地址。 这可能是由于驱动程序将项排队到系统工作线程。

此驱动程序需要符合终端服务器的内存管理规则。

 

 




