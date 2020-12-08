---
title: Bug 检查 0xEB DIRTY_MAPPED_PAGES_CONGESTION
description: DIRTY_MAPPED_PAGES_CONGESTION bug 检查的值为0x000000EB。 这表示无可用页面可用于继续操作。
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
ms.openlocfilehash: 586b1fc999f7b93b2c698d39f433dee1d20ea036
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793259"
---
# <a name="bug-check-0xeb-dirty_mapped_pages_congestion"></a>Bug 检查0xEB：脏 \_ 映射 \_ 页 \_ 拥塞


脏 \_ 映射 \_ 页 \_ 拥塞 bug 检查的值为0x000000EB。 这表示无可用页面可用于继续操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="dirty_mapped_pages_congestion-parameters"></a>脏 \_ 映射 \_ 页 \_ 拥塞参数


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
<td align="left"><p>发往页面文件的脏页数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>仅适用于 Windows Server 2003： bug 检查时可用的非分页池的大小 (页面) </p>
<p>Windows Vista 及更高版本：保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>仅限 Windows Server 2003：当前闲置的转换页数</p>
<p>Windows Vista 及更高版本：最新修改的写入错误状态</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

文件系统驱动程序堆栈有死锁，并且大部分修改的页面都发送到文件系统。 由于文件系统不可操作，因此系统崩溃，因为在不丢失数据的情况下，不能重复使用任何修改的页面。 堆栈中的任何文件系统或筛选器驱动程序可能出错。

若要查看一般内存统计信息，请使用 [**！ vm 3**](-vm.md) 扩展。

由于以下任一原因，可能会发生此错误检查：

-   驱动程序已阻止，死锁已修改或映射的页编写器。 这种情况的示例包括互斥锁或对文件系统驱动程序或筛选器驱动程序中的内存分页的访问。 这表明驱动程序 bug。

    如果参数1或参数2很大，则可能会出现这种情况。 使用 [**！ vm 3**](-vm.md)。

-   存储驱动程序未处理请求。 这种情况的示例包括：闲置队列和无响应驱动器。 这表明驱动程序 bug。

    如果参数1或参数2很大，则可能会出现这种情况。 使用 [**！进程 0 7**](-process.md)。

-   仅限 Windows Server 2003：没有足够的池可用于存储堆栈，无法写出已修改的页面。 这表明驱动程序 bug。

    如果参数3很小，则可能出现这种情况。 使用 [**！ vm**](-vm.md) 和 [**！ poolused 2**](-poolused.md)。

 

 




