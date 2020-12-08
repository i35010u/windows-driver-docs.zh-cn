---
title: Bug 检查 0xEC SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT
description: SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT bug 检查的值为0x000000EC。 这表示会话驱动程序仍保留在内存中时，发生了会话卸载。
keywords:
- Bug 检查 0xEC SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT
- SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c7c48aea9128e303f7f30222db419e4e758e011
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793257"
---
# <a name="bug-check-0xec-session_has_valid_special_pool_on_exit"></a>Bug 检查0xEC：会话 \_ \_ \_ \_ \_ 在 \_ 退出时具有有效的特殊池


会话 \_ 具有 \_ \_ \_ \_ 对 \_ 退出 bug 的有效特殊池错误检查的值为0x000000EC。 这表示会话驱动程序仍保留在内存中时，发生了会话卸载。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="session_has_valid_special_pool_on_exit-parameters"></a>会话 \_ \_ \_ \_ \_ 在 \_ EXIT 参数上具有有效的特殊池


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
<td align="left"><p>泄漏的特殊池页的数目</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误是由会话驱动程序在会话卸载之前未释放其特殊池分配导致的。 这表示 win32k.sys、atmfd.dll、rdpdd.dll 或视频驱动程序中的 bug。

 

 




