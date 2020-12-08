---
title: Bug 检查 0x51 REGISTRY_ERROR
description: REGISTRY_ERROR bug 检查的值为0x00000051。 这表明出现了严重的注册表错误。
keywords:
- Bug 检查 0x51 REGISTRY_ERROR
- REGISTRY_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REGISTRY_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 789838f177f9272dffe18d8995bb11c96b47a1c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786465"
---
# <a name="bug-check-0x51-registry_error"></a>Bug 检查0x51：注册表 \_ 错误


注册表 \_ 错误错误检查的值为0x00000051。 这表明出现了严重的注册表错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="registry_error-parameters"></a>注册表 \_ 错误参数


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
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>指向 hive (的指针（如果可用）) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>如果该配置单元已损坏， <strong>HvCheckHive</strong> 的返回代码 (（如果可用）) </p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

注册表出现问题。 如果内核调试器可用，则获取堆栈跟踪： " [**！分析**](-analyze.md) " 调试扩展显示有关 bug 检查的信息，并且在确定根本原因时可能非常有用，然后输入一个 " [**k (" 显示堆栈 Backtrace ")**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) " 命令，以查看调用堆栈。

此错误可能表示注册表在尝试读取其某个文件时遇到 i/o 错误。 这可能是由硬件问题或文件系统损坏引起的。

这也可能是因为在刷新操作中失败，后者仅在由安全系统使用，并仅在遇到资源限制时出现。

 

 




