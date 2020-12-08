---
title: Bug 检查 0x10F RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
description: RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED bug 检查的值为0x0000010F。
keywords:
- Bug 检查 0x10F RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
- RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a63d4c2bdc02a0ef9c37e2603179eacb3df3eb7f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790059"
---
# <a name="bug-check-0x10f-resource_manager_exception_not_handled"></a>Bug 检查0x10F：资源 \_ 管理器 \_ 异常 \_ 未 \_ 处理


资源 \_ 管理器 \_ 异常 \_ 未 \_ 处理 bug 检查的值为0x0000010F。 这表示内核事务管理器检测到内核模式资源管理器已引发异常来响应直接回拨。 资源管理器处于意外且不可恢复的状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="resource_manager_exception_not_handled-parameters"></a>资源 \_ 管理器 \_ 异常 \_ 未处理的 \_ 参数


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
<td align="left"><p>异常记录的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>上下文记录的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>异常代码的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>资源管理器的地址</p></td>
</tr>
</tbody>
</table>

 

 

 




