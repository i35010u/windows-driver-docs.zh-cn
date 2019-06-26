---
title: Bug 检查 0x92 UP_DRIVER_ON_MP_SYSTEM
description: UP_DRIVER_ON_MP_SYSTEM bug 检查具有 0x00000092 值。 此 bug 检查指示，已在多处理器系统上加载，仅限单处理器的驱动程序。
ms.assetid: 1e26c7b1-bfa5-4a32-a483-5ce8179ac6b7
keywords:
- Bug 检查 0x92 UP_DRIVER_ON_MP_SYSTEM
- UP_DRIVER_ON_MP_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- UP_DRIVER_ON_MP_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: caa3247387e2fa391b1feeac127f7f3e9a19877a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367283"
---
# <a name="bug-check-0x92-updriveronmpsystem"></a>Bug 检查 0x92：UP\_DRIVER\_ON\_MP\_SYSTEM


向上\_驱动程序\_ON\_MP\_检查系统错误的值为 0x00000092。 此 bug 检查指示，已在多处理器系统上加载，仅限单处理器的驱动程序。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="updriveronmpsystem-parameters"></a>向上\_驱动程序\_ON\_MP\_系统参数


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
<td align="left"><p>驱动程序的基址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
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

已加载的驱动程序，编译若要仅在单处理器计算机上运行，但具有多个活动处理器的多处理器系统上运行 Microsoft Windows 操作系统。

 
## <a name="resolution"></a>分辨率
[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。




