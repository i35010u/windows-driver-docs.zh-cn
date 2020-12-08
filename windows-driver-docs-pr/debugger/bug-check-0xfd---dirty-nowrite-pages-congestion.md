---
title: Bug 检查 0xFD DIRTY_NOWRITE_PAGES_CONGESTION
description: DIRTY_NOWRITE_PAGES_CONGESTION bug 检查的值为0x000000FD。 这表明没有可用的页面来继续基本系统操作。
keywords:
- Bug 检查 0xFD DIRTY_NOWRITE_PAGES_CONGESTION
- DIRTY_NOWRITE_PAGES_CONGESTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DIRTY_NOWRITE_PAGES_CONGESTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c06db1ce40e3cde970157cabefdfcce832270415
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819245"
---
# <a name="bug-check-0xfd-dirty_nowrite_pages_congestion"></a>Bug 检查0xFD：脏 \_ NOWRITE \_ PAGES \_ 拥塞


脏 \_ NOWRITE \_ PAGES \_ 拥塞 bug 检查的值为0x000000FD。 这表明没有可用的页面来继续基本系统操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="dirty_nowrite_pages_congestion-parameters"></a>脏 \_ NOWRITE \_ PAGES \_ 拥塞参数


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
<td align="left"><p>脏页总数</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>不可写入脏页的数目</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>最近修改的写入错误状态</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

通常会发生此错误检查，因为在将相关文件标记为 "不写入" 内存管理后，拥有已修改的非可写页面的组件未能写出这些页面。 这表明驱动程序 bug。

<a name="resolution"></a>解决方法
----------

有关哪个驱动程序导致了该问题的详细信息，请使用 [**！ vm 3**](-vm.md) 扩展，后跟 [**！ memusage 1**](-memusage.md) 。

 

 




