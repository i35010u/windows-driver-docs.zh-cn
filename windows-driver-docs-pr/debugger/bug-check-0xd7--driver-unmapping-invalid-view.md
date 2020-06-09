---
title: Bug 检查 0xD7 DRIVER_UNMAPPING_INVALID_VIEW
description: DRIVER_UNMAPPING_INVALID_VIEW bug 检查的值为0x000000D7。 这表明驱动程序正在尝试取消对未映射的地址的映射。
ms.assetid: 68075aa7-f579-49c7-a30a-a21312625ff9
keywords:
- Bug 检查 0xD7 DRIVER_UNMAPPING_INVALID_VIEW
- DRIVER_UNMAPPING_INVALID_VIEW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_UNMAPPING_INVALID_VIEW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c69a4233e26bbeca5d5d52141b2b92c29331f7cb
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534540"
---
# <a name="bug-check-0xd7-driver_unmapping_invalid_view"></a>Bug 检查0xD7：驱动程序取消 \_ 映射 \_ 无效 \_ 视图


驱动程序取消 \_ 映射 \_ 无效 \_ 的视图 bug 检查的值为0x000000D7。 这表明驱动程序正在尝试取消对未映射的地址的映射。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="driver_unmapping_invalid_view-parameters"></a>驱动程序取消 \_ 映射 \_ 无效的 \_ 视图参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>要取消映射的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>1：</strong>正在取消映射视图</p>
<p><strong>2：</strong>正在提交视图</p></td>
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

 

<a name="remarks"></a>注解
-------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。 使用[**kb （显示 Stack Backtrace）**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令获取堆栈跟踪：可以从堆栈跟踪确定导致错误的驱动程序。

 

 




