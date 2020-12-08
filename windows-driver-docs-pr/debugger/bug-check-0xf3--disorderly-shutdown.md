---
title: Bug 检查 0xF3 DISORDERLY_SHUTDOWN
description: DISORDERLY_SHUTDOWN bug 检查的值为0x000000F3。 这表示由于内存不足，Windows 无法关闭。
keywords:
- Bug 检查 0xF3 DISORDERLY_SHUTDOWN
- DISORDERLY_SHUTDOWN
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DISORDERLY_SHUTDOWN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d38ed7f3ac4d7a38dc20be53ddcef7a167fa042
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827359"
---
# <a name="bug-check-0xf3-disorderly_shutdown"></a>Bug 检查0xF3： DISORDERLY \_ 关闭


DISORDERLY \_ 关闭 bug 检查的值为0x000000F3。 这表示由于内存不足，Windows 无法关闭。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="disorderly_shutdown-parameters"></a>DISORDERLY \_ 关闭参数


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
<p>Windows Vista 和更高版本：保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>仅限 Windows Server 2003：当前的关闭阶段</p>
<p>Windows Vista 及更高版本：最新修改的写入错误状态</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Windows 尝试关闭，但没有可用于继续操作的免费页面。

由于应用程序未终止并且未卸载驱动程序，因此即使修改后的编写器已终止，它们仍会继续访问页。 这会导致系统用尽页面，因为可以使用页文件。

 

 




