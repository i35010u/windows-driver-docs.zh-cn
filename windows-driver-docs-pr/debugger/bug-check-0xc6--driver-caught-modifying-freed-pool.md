---
title: Bug 检查 0xC6 DRIVER_CAUGHT_MODIFYING_FREED_POOL
description: DRIVER_CAUGHT_MODIFYING_FREED_POOL bug 检查的值为0x000000C6。 这表明驱动程序尝试访问已释放的内存池。
keywords:
- Bug 检查 0xC6 DRIVER_CAUGHT_MODIFYING_FREED_POOL
- DRIVER_CAUGHT_MODIFYING_FREED_POOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CAUGHT_MODIFYING_FREED_POOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3055ab0a2e26e8d06ff3dea3b21de0aa2176aca7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838671"
---
# <a name="bug-check-0xc6-driver_caught_modifying_freed_pool"></a>Bug 检查0xC6：驱动程序已 \_ 捕获 \_ 修改已释放的 \_ \_ 池


捕获的驱动程序 \_ \_ 修改 \_ \_ 已释放的池 bug 检查的值为0x000000C6。 这表明驱动程序尝试访问已释放的内存池。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_caught_modifying_freed_pool-parameters"></a>已 \_ 捕获驱动程序 \_ 修改 \_ 释放的 \_ 池参数


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
<td align="left"><p>引用的内存</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0：</strong> 读取</p>
<p><strong>1：</strong> 写入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0：</strong> 内核模式</p>
<p><strong>1：</strong> 用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

出现故障的组件将显示在当前内核堆栈中。 应该替换或调试此驱动程序。

 

 




