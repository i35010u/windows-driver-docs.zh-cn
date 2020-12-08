---
title: Bug 检查 0xAB SESSION_HAS_VALID_POOL_ON_EXIT
description: SESSION_HAS_VALID_POOL_ON_EXIT bug 检查的值为0x000000AB。 此 bug 检查表明会话驱动程序仍保留内存时，发生了会话卸载。
keywords:
- Bug 检查 0xAB SESSION_HAS_VALID_POOL_ON_EXIT
- SESSION_HAS_VALID_POOL_ON_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SESSION_HAS_VALID_POOL_ON_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c32d1bb66edfa99b9bf28fe7d984f42c86377fc7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784153"
---
# <a name="bug-check-0xab-session_has_valid_pool_on_exit"></a>Bug 检查0xAB：会话 \_ \_ \_ \_ 在退出时具有有效的池 \_


会话 \_ 具有 \_ 无效 \_ \_ \_ 的退出 bug 检查池，其值为0x000000AB。 此 bug 检查表明会话驱动程序仍保留内存时，发生了会话卸载。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="session_has_valid_pool_on_exit-parameters"></a>会话 \_ 具有 \_ 无效 \_ \_ 的 \_ 退出参数池


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
<td align="left"><p>会话 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>正在泄漏的分页池字节数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>正在泄漏的非分页缓冲池字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>正在泄漏的分页和非分页分配的总数。  (此词上半部分的非分页分配数，分页分配在此词的下半部分。 ) </p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

由于会话 \_ \_ \_ \_ \_ 驱动程序在会话卸载之前不释放其池分配，因此会话具有有效的退出 bug 检查池。 此 bug 检查可指示 Win32k.sys、Atmfd.dll、Rdpdd.dll 或视频或其他驱动程序中的 bug。

 

 




