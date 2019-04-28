---
title: Bug 检查 0xF3 DISORDERLY_SHUTDOWN
description: DISORDERLY_SHUTDOWN bug 检查具有 0x000000F3 值。 这表示 Windows 无法关闭由于内存不足的情况下。
ms.assetid: e113cd2f-96b2-43b8-a67e-a851cc5c0da8
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
ms.openlocfilehash: 670a60f3a91c281eafd80048ca845853fcf2c39b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342096"
---
# <a name="bug-check-0xf3-disorderlyshutdown"></a>Bug 检查 0xF3：DISORDERLY\_关闭


DISORDERLY\_关闭 bug 检查的值为 0x000000F3。 这表示 Windows 无法关闭由于内存不足的情况下。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="disorderlyshutdown-parameters"></a>DISORDERLY\_关闭参数


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
<p>Windows Vista 及更高版本：保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>仅 Windows Server 2003 计算机：当前关闭的情况下阶段</p>
<p>Windows Vista 及更高版本：最新的修改后的写入错误状态</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Windows 尝试关闭的情况下，但没有任何可用的空闲页以继续操作。

应用程序已不终止并且驱动程序已不卸载，因为它们继续甚至修改后的编写器必须终止后访问页面。 这会导致系统运行页，因为无法使用页文件。

 

 




