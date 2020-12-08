---
title: Bug 检查 0xA2 MEMORY_IMAGE_CORRUPT
description: MEMORY_IMAGE_CORRUPT bug 检查的值为0x000000A2。 此 bug 检查指示在内存中的可执行文件的映像中检测到损坏。
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
ms.openlocfilehash: 708c4e99f086df1d6061eb0117b6a62f935cd2f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819251"
---
# <a name="bug-check-0xa2-memory_image_corrupt"></a>Bug 检查0xA2：内存 \_ 映像 \_ 已损坏


内存 \_ 映像 \_ 损坏 bug 检查的值为0x000000A2。 此 bug 检查指示在内存中的可执行文件的映像中检测到损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="memory_image_corrupt-parameters"></a>内存 \_ 映像 \_ 损坏参数


参数1指示违规类型。 其他参数的意义取决于参数1的值。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p><strong>如果参数3为零：</strong> 表页中失败的页码</p>
<p><strong>如果参数3不为零：</strong> 页面上包含失败页的运行索引</p></td>
<td align="left"><p>零或无法匹配运行的索引</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>出现表页检查失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>范围的起始物理页码</p></td>
<td align="left"><p>范围)  (的长度</p></td>
<td align="left"><p>包含此运行的表页的页码</p></td>
<td align="left"><p>列出的内存范围不正确。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

对内存范围 (CRC) 检查的循环冗余检查已失败。

在系统唤醒操作中，可能会检查各种内存区域，以防出现内存故障。

 

 




