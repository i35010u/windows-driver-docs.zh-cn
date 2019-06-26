---
title: Bug 检查 0x105 AGP_GART_CORRUPTION
description: AGP_GART_CORRUPTION bug 检查具有 0x00000105 值。 这表示图形 Aperture 重新映射表 (GART) 已损坏。
ms.assetid: efc39d1f-666d-4377-a262-ed5164357b52
keywords:
- Bug 检查 0x105 AGP_GART_CORRUPTION
- AGP_GART_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AGP_GART_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: acc01c751aadaa75a220d8b2abb0a1a1ee44ad60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367953"
---
# <a name="bug-check-0x105-agpgartcorruption"></a>Bug 检查 0x105：AGP\_GART\_损坏


AGP\_GART\_损坏错误检查的值为 0x00000105。 这表示图形 Aperture 重新映射表 (GART) 已损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="agpgartcorruption-parameters"></a>AGP\_GART\_损坏参数


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
<td align="left"><p>基址 （虚拟） 的 GART</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>发生损坏 GART 中的偏移量</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>基址 （虚拟） 的 GART 缓存 （一份 GART）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

检查此错误通常是由不正确的直接内存访问 (DMA) 由驱动程序引起的。

<a name="resolution"></a>分辨率
----------

为任何未签名的驱动程序启用驱动程序验证程序。 将其删除或禁用逐个进行，直到找出 erring 驱动程序。

 

 




