---
title: Bug 检查 0x122 WHEA_INTERNAL_ERROR
description: WHEA_INTERNAL_ERROR bug 检查的值为0x00000122。
keywords:
- Bug 检查 0x122 WHEA_INTERNAL_ERROR
- WHEA_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WHEA_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dcfd7aefe700b13f7715f1c1ee36977af9727185
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787962"
---
# <a name="bug-check-0x122-whea_internal_error"></a>Bug 检查0x122： WHEA \_ 内部 \_ 错误


WHEA \_ 内部 \_ 错误 bug 检查的值为0x00000122。 此 bug 检查表明出现 Windows 硬件错误体系结构中的内部错误 (WHEA) 。 错误可能是由供应商提供的特定于平台的硬件错误驱动程序的实现中的错误导致的， (PSHED 提供商提供的) 插件、错误记录的固件实现或错误注入的固件实现。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="whea_internal_error-parameters"></a>WHEA \_ 内部 \_ 错误参数


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
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>内存大小</p></td>
<td align="left"><p>错误源计数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法为硬件错误源表中的所有错误源分配足够的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>处理器数目</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法为每个处理器的 WHEA 信息块分配足够的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>状态</p></td>
<td align="left"><p>阶段 (bug 检查的初始化阶段) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>WHEA 无法分配足够的内存用于错误源，或错误源枚举失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>状态</p></td>
<td align="left"><p>阶段</p></td>
<td align="left"><p>错误源类型</p></td>
<td align="left"><p>未能初始化参数3所指定阶段 (参数 4) 的错误源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>状态</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>未能分配足够的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>错误源的数目</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法为所有错误源描述符分配足够的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>错误源类型</p></td>
<td align="left"><p>源 ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>WHEA 收到了来自无效错误源的未更正的错误源。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>错误源类型</p></td>
<td align="left"><p>源 ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法为未更正的错误分配错误记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xB</p></td>
<td align="left"><p>错误源类型</p></td>
<td align="left"><p>源 ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法为未更正的错误填充错误记录。</p></td>
</tr>
</tbody>
</table>

 

如果参数1等于0x6、0x9、0xA 或0xB，则其中一个参数包含错误源类型。 下表提供了错误源类型的可能值。

| “值” | 描述                          |
|-------|--------------------------------------|
| 0x00  | 计算机检查异常              |
| 0x01  | 已更正计算机检查              |
| 0x02  | 更正了平台错误             |
| 0x03  | 不可屏蔽中断               |
| 0x04  | PCI express 错误                    |
| 0x05  | 其他类型的错误源/泛型 |
| 0x06  | IA64 初始化错误源               |
| 0x07  | 启动错误源                    |
| 0x08  | 基于科幻的通用错误源       |
| 0x09  | Itanium 计算机检查中止          |
| 0x0A  | Itanium 计算机检查                |
| 0x0B  | 安腾更正平台错误     |

 

 

 




