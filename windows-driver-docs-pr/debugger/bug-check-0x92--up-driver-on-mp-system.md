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
ms.openlocfilehash: e4e79cf978d7cbfb26cc8efecd78fe3aef6177ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564523"
---
# <a name="bug-check-0x92-updriveronmpsystem"></a>Bug 检查 0x92：UP\_DRIVER\_ON\_MP\_SYSTEM


向上\_驱动程序\_ON\_MP\_检查系统错误的值为 0x00000092。 此 bug 检查指示，已在多处理器系统上加载，仅限单处理器的驱动程序。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

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

 

 




