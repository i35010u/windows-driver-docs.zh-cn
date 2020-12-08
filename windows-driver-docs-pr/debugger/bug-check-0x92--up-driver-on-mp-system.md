---
title: Bug 检查 0x92 UP_DRIVER_ON_MP_SYSTEM
description: UP_DRIVER_ON_MP_SYSTEM bug 检查的值为0x00000092。 此错误检查指示已在多处理器系统上加载仅限单处理器的驱动程序。
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
ms.openlocfilehash: 64f41e3e082dc11e050966656cd08dacb5fe7bcb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822597"
---
# <a name="bug-check-0x92-up_driver_on_mp_system"></a>Bug 检查0x92： \_ \_ \_ MP 系统上的驱动程序 \_


\_ \_ MP 系统上的驱动程序 \_ \_ bug 检查的值为0x00000092。 此错误检查指示已在多处理器系统上加载仅限单处理器的驱动程序。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="up_driver_on_mp_system-parameters"></a>\_ \_ MP 系统上的驱动程序 \_ \_ 参数


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
<td align="left"><p>预留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

已编译为仅在单处理器计算机上使用的驱动程序已加载，但 Microsoft Windows 操作系统正在具有多个活动处理器的多处理器系统上运行。

 
## <a name="resolution"></a>解决方法
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。




