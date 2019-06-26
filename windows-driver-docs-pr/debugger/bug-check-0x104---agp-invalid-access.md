---
title: Bug 检查 0x104 AGP_INVALID_ACCESS
description: AGP_INVALID_ACCESS bug 检查具有 0x00000104 值。 这表示 GPU 编写到范围的加速图形不以前已提交的端口 (AGP) 内存。
ms.assetid: c1f5322e-847a-424f-b117-1714b8572a4f
keywords:
- Bug 检查 0x104 AGP_INVALID_ACCESS
- AGP_INVALID_ACCESS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AGP_INVALID_ACCESS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3b309d58b6a386a4092bc50d732fcab4a01d3e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362355"
---
# <a name="bug-check-0x104-agpinvalidaccess"></a>Bug 检查 0x104：AGP\_无效\_访问


AGP\_无效\_访问错误检查的值为 0x00000104。 这表示 GPU 编写到范围的加速图形不以前已提交的端口 (AGP) 内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="agpinvalidaccess-parameters"></a>AGP\_无效\_访问参数


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
<td align="left"><p>偏移量 （以 ULONG) 内 AGP verifier 页已损坏的第一个 ULONG 数据</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

通常情况下，此 bug 检查引起的无符号或不正确经过测试的视频驱动程序。 它还可能引起较旧的 BIOS。

<a name="resolution"></a>分辨率
----------

检查显示驱动程序和计算机 BIOS 更新。

 

 




