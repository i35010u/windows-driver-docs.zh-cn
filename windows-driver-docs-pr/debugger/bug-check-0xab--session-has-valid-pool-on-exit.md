---
title: Bug 检查 0xAB SESSION_HAS_VALID_POOL_ON_EXIT
description: SESSION_HAS_VALID_POOL_ON_EXIT bug 检查具有 0x000000AB 值。 此 bug 检查指示会话卸载时发生会话驱动程序仍保留内存中。
ms.assetid: fe4587cc-2567-4452-a3e7-22a53def76b2
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
ms.openlocfilehash: 7196d3521573b4b97792400e06901721d3fe9394
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239796"
---
# <a name="bug-check-0xab-sessionhasvalidpoolonexit"></a>Bug 检查 0xAB：会话\_HAS\_有效\_池\_ON\_退出


会话\_HAS\_有效\_池\_ON\_退出 bug 检查的值为 0x000000AB。 此 bug 检查指示会话卸载时发生会话驱动程序仍保留内存中。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="sessionhasvalidpoolonexit-parameters"></a>会话\_HAS\_有效\_池\_ON\_退出参数


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
<td align="left"><p>会话 id。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>泄漏的分页的池字节数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>泄漏的非分页的池字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>泄漏的分页和非分页分配的总数。 （非分页的分配数是此词的上半部分和分页的分配是该单词的下半部分。）</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

会话\_HAS\_有效\_池\_ON\_退出 bug 检查出现的原因会话驱动程序不会释放会话卸载前的其池分配。 此 bug 检查可以指示 Win32k.sys、 Atmfd.dll、 Rdpdd.dll 或视频或其他驱动程序中的 bug。

 

 




