---
title: Bug 检查 0xEB DIRTY_MAPPED_PAGES_CONGESTION
description: DIRTY_MAPPED_PAGES_CONGESTION bug 检查具有 0x000000EB 值。 这表明没有可用的空闲页是可用于继续操作。
ms.assetid: 7a73dc74-fe40-4c0c-9c33-b0af3709bf43
keywords:
- Bug 检查 0xEB DIRTY_MAPPED_PAGES_CONGESTION
- DIRTY_MAPPED_PAGES_CONGESTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DIRTY_MAPPED_PAGES_CONGESTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: edfdb453ecba8934ed8bdc9e97da6886abc64b51
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239396"
---
# <a name="bug-check-0xeb-dirtymappedpagescongestion"></a>Bug 检查 0xEB：脏\_映射\_页面\_拥塞


DIRTY\_映射\_页面\_拥塞 bug 检查的值为 0x000000EB。 这表明没有可用的空闲页是可用于继续操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="dirtymappedpagescongestion-parameters"></a>脏\_映射\_页面\_拥塞参数


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
<td align="left"><p>为页面文件发送到的损坏页的数量</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>仅 Windows Server 2003 计算机：签入的 bug （页） 时可用的非分页池的大小</p>
<p>Windows Vista 和更高版本：保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>仅 Windows Server 2003 计算机：当前闲置的转换页面数</p>
<p>Windows Vista 和更高版本：最新的修改后的写入错误状态</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

文件系统驱动程序堆栈已发生死锁和已修改页的大多数目标为文件系统。 由于文件系统是不可操作状态，系统已崩溃，因为没有任何已修改页可以重复使用而不会丢失数据。 堆栈中的任何文件系统或筛选器驱动程序可能有故障。

若要查看常规内存统计信息，请使用[ **！ vm 3** ](-vm.md)扩展。

此 bug 检查可能发生以下情况之一：

-   已阻止驱动程序，死锁已修改或映射页编写器。 此示例包括互斥锁死锁或访问文件系统驱动程序或筛选器驱动程序中的内存分页。 这指示驱动程序 bug。

    如果参数 1 或参数 2 很大，可能会这样。 使用[ **！ vm 3**](-vm.md)。

-   存储驱动程序不处理请求。 此方面的示例是孤立的队列和无响应的驱动器。 这指示驱动程序 bug。

    如果参数 1 或参数 2 很大，可能会这样。 使用[ **！ 处理 0 7**](-process.md)。

-   仅 Windows Server 2003 计算机：没有足够的池是可用于存储堆栈，写出已修改页。 这指示驱动程序 bug。

    如果参数 3 很小，这可能会。 使用[ **！ vm** ](-vm.md)并[ **！ poolused 2**](-poolused.md)。

 

 




