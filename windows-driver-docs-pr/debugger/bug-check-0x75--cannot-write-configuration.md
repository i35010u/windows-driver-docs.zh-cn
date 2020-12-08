---
title: Bug 检查 0x75 CANNOT_WRITE_CONFIGURATION
description: CANNOT_WRITE_CONFIGURATION bug 检查的值为0x00000075。 此 bug 检查指示系统注册表配置单元文件无法转换为映射文件。
keywords:
- Bug 检查 0x75 CANNOT_WRITE_CONFIGURATION
- CANNOT_WRITE_CONFIGURATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CANNOT_WRITE_CONFIGURATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 77974b1d78a54255d1cacad524582f610b10c7e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787017"
---
# <a name="bug-check-0x75-cannot_write_configuration"></a>Bug 检查0x75：无法 \_ 写入 \_ 配置


"无法 \_ 写入 \_ 配置 bug 检查" 的值为 "0x00000075"。 此 bug 检查指示系统注册表配置单元文件无法转换为映射文件。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="cannot_write_configuration-parameters"></a>无法 \_ 写入 \_ 配置参数


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
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>导致 Windows 操作系统无法转换配置单元的 NT 状态代码。</p></td>
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

\_ \_ 如果系统不在池中并且 Windows 操作系统无法重新打开 hive，则通常会发生 "无法写入配置 bug 检查"。

此 bug 检查几乎不会发生，因为在系统初始化过程中，hive 文件的转换提前完成，以便足以提供足够的池。

 

 




