---
title: Bug 检查 0xEC SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT
description: SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT bug 检查具有 0x000000EC 值。 这指示会话卸载时发生会话驱动程序仍保留内存中。
ms.assetid: 0100684b-cde6-4f15-93da-78d200fa2f80
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
ms.openlocfilehash: a5b9e9c2cf6e787dc757648ed9d26761cad59000
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902905"
---
# <a name="bug-check-0xec-sessionhasvalidspecialpoolonexit"></a>Bug 检查 0xEC：会话\_HAS\_有效\_特殊\_池\_ON\_退出


会话\_HAS\_有效\_特殊\_池\_ON\_退出 bug 检查的值为 0x000000EC。 这指示会话卸载时发生会话驱动程序仍保留内存中。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="sessionhasvalidspecialpoolonexit-parameters"></a>会话\_HAS\_有效\_特殊\_池\_ON\_退出参数


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
<td align="left"><p>泄漏的特殊池页面数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

未在释放会话卸载之前其特殊的池分配一个会话驱动程序导致此错误。 这表示 win32k.sys、 atmfd.dll、 rdpdd.dll 或视频驱动程序中的 bug。

 

 




