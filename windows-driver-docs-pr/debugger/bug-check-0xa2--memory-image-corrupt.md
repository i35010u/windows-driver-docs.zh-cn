---
title: Bug 检查 0xA2 MEMORY_IMAGE_CORRUPT
description: MEMORY_IMAGE_CORRUPT bug 检查具有 0x000000A2 值。 检查此错误指示在内存中的可执行文件的图像中检测到损坏。
ms.assetid: 73990217-4af2-478c-aa5e-39e6bc5811cf
keywords:
- Bug 检查 0xA2 MEMORY_IMAGE_CORRUPT
- MEMORY_IMAGE_CORRUPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MEMORY_IMAGE_CORRUPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0f3bd43c82a8b6f16041eec070511ae3548c9329
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567330"
---
# <a name="bug-check-0xa2-memoryimagecorrupt"></a>Bug 检查 0xA2：内存\_图像\_损坏


内存\_图像\_损坏错误检查的值为 0x000000A2。 检查此错误指示在内存中的可执行文件的图像中检测到损坏。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="memoryimagecorrupt-parameters"></a>内存\_图像\_损坏参数


参数 1 指示冲突的类型。 其他参数的含义取决于参数 1 的值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p><strong>如果参数 3 为零：</strong>中失败的表页的页码</p>
<p><strong>如果参数 3 为非零值：</strong>与运行索引失败页的页码</p></td>
<td align="left"><p>零或无法匹配运行的索引</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>表页上检查失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>范围的起始的物理页号</p></td>
<td align="left"><p>范围的长度 （以页）</p></td>
<td align="left"><p>包含此运行表页的页码</p></td>
<td align="left"><p>列出的内存范围的校验和不正确。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

内存范围内的循环冗余校验 (CRC) 检查失败。

系统唤醒操作时，可能会检查各个区域的内存以防止出现内存故障。

 

 




