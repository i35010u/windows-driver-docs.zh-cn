---
title: Bug 检查 0x122 WHEA_INTERNAL_ERROR
description: WHEA_INTERNAL_ERROR bug 检查具有 0x00000122 值。
ms.assetid: b0bf1f27-bfdd-4d5d-aeac-f74f45c6174f
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
ms.openlocfilehash: 80ba9814fa753bef08cc0a8ffcfdcdb500321e8b
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520784"
---
# <a name="bug-check-0x122-wheainternalerror"></a>Bug 检查 0x122：WHEA\_INTERNAL\_ERROR


WHEA\_内部\_错误 bug 检查的值为 0x00000122。 此 bug 检查指示已发生内部错误在 Windows 硬件错误体系结构 (WHEA)。 由供应商、 错误记录的固件实现或错误注入的固件实现提供特定于平台的硬件错误驱动程序 (PSHED) 插件实现中的 bug 可能会导致错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="wheainternalerror-parameters"></a>WHEA\_内部\_错误参数


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
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>内存的大小</p></td>
<td align="left"><p>错误源计数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法分配足够的内存硬件错误源表中的所有错误源。</p></td>
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
<td align="left"><p>阶段 （错误检查初始化阶段）</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>WHEA 错误源，或失败的错误源枚举分配足够的内存失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>状态</p></td>
<td align="left"><p>阶段</p></td>
<td align="left"><p>错误源类型</p></td>
<td align="left"><p>无法初始化指定的参数 3 在阶段错误源 (参数 4)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>状态</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法分配足够的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>错误源数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法分配足够的内存，所有错误的源描述符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>错误源类型</p></td>
<td align="left"><p>源 ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>WHEA 从无效的错误源接收未更正的错误源。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>错误源类型</p></td>
<td align="left"><p>源 ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法分配得出未修正错误的错误记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xB</p></td>
<td align="left"><p>错误源类型</p></td>
<td align="left"><p>源 ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法填充得出未修正错误的错误记录。</p></td>
</tr>
</tbody>
</table>

 

如果参数 1 为 0x6、 0x9、 0xA 或 0xB，其他参数之一包含错误源类型。 下表给出的错误源类型的可能的值。

| 值 | 描述                          |
|-------|--------------------------------------|
| 0x00  | 计算机检查异常              |
| 0x01  | 更正计算机检查              |
| 0x02  | 已更正的平台错误             |
| 0x03  | 不可屏蔽的中断               |
| 0x04  | PCI express 错误                    |
| 0x05  | 其他类型的错误源/泛型 |
| 0x06  | IA64 INIT 错误源               |
| 0x07  | 启动错误源                    |
| 0x08  | 基于名工商管理学博士的一般性错误源       |
| 0x09  | Itanium 计算机检查中止          |
| 0x0A  | Itanium 计算机检查                |
| 0x0B  | Itanium 更正平台错误     |

 

 

 




