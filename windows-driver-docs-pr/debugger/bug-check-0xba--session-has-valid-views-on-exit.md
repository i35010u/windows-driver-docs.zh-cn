---
title: Bug 检查 0xBA SESSION_HAS_VALID_VIEWS_ON_EXIT
description: SESSION_HAS_VALID_VIEWS_ON_EXIT bug 检查的值为0x000000BA。 这表示会话驱动程序在卸载会话时仍具有映射视图。
keywords:
- Bug 检查 0xBA SESSION_HAS_VALID_VIEWS_ON_EXIT
- SESSION_HAS_VALID_VIEWS_ON_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SESSION_HAS_VALID_VIEWS_ON_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c3e5e19932e19f9502b7c2b15ea7c859179be2b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838241"
---
# <a name="bug-check-0xba-session_has_valid_views_on_exit"></a>Bug 检查0xBA：会话 \_ \_ \_ \_ 在退出时具有有效的视图 \_


会话 \_ 具有 \_ \_ \_ 对退出 bug 检查的有效视图， \_ 其值为0x000000BA。 这表示会话驱动程序在卸载会话时仍具有映射视图。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="session_has_valid_views_on_exit-parameters"></a>会话 \_ \_ \_ \_ 在 \_ 退出参数上具有有效的视图


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
<td align="left"><p>会话 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>正在泄漏的映射视图数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>此会话的映射视图表的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>此会话的映射视图表的大小</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误是由会话驱动程序在会话卸载之前未映射其映射视图导致的。 这表示 win32k.sys、atmfd.dll、rdpdd.dll 或视频驱动程序中的 bug。

 

 




