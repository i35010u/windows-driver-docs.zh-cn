---
title: Bug 检查 0xFD DIRTY_NOWRITE_PAGES_CONGESTION
description: DIRTY_NOWRITE_PAGES_CONGESTION bug 检查具有 0x000000FD 值。 这指示没有可用的空闲页继续基本系统操作。
ms.assetid: b657fffe-8331-4b4f-9d29-fea8ee1e1682
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
ms.openlocfilehash: b8f09eefeeccc5f5a292659bd7abea64671fc0b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567498"
---
# <a name="bug-check-0xfd-dirtynowritepagescongestion"></a>Bug 检查 0xFD：脏\_非写入\_页面\_拥塞


DIRTY\_非写入\_页面\_拥塞 bug 检查的值为 0x000000FD。 这指示没有可用的空闲页继续基本系统操作。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="dirtynowritepagescongestion-parameters"></a>脏\_非写入\_页面\_拥塞参数


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
<td align="left"><p>脏页的总数</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>非可写的脏页的数量</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>最最近修改过的写入错误状态</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

由于拥有已修改非可写页组件无法写出这些页面进行内存管理标记为"不写入"相关的文件后，通常会出现此 bug 检查。 这指示驱动程序 bug。

<a name="resolution"></a>分辨率
----------

有关详细信息有关的驱动程序导致了问题，使用[ **！ vm 3** ](-vm.md)扩展后, 跟[ **！ memusage 1** ](-memusage.md) 。

 

 




