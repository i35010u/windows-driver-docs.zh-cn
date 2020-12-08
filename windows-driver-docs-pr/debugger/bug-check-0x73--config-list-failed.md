---
title: Bug 检查 0x73 CONFIG_LIST_FAILED
description: CONFIG_LIST_FAILED bug 检查的值为0x00000073。 此 bug 检查表明无法在注册表树中链接顶级注册表项，也称为核心系统配置单元。
keywords:
- Bug 检查 0x73 CONFIG_LIST_FAILED
- CONFIG_LIST_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CONFIG_LIST_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff76faccc1d234ec32d2d8e9605f9a880242169d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787025"
---
# <a name="bug-check-0x73-config_list_failed"></a>Bug 检查0x73：配置 \_ 列表 \_ 失败


配置 \_ 列表 \_ 失败 bug 检查的值为0x00000073。 此 bug 检查表明无法在注册表树中链接顶级注册表项，也称为核心系统配置单元。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="config_list_failed-parameters"></a>配置 \_ 列表 \_ 失败参数


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
<td align="left"><p>导致 Windows 操作系统无法加载配置单元的 NT 状态代码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>Hive 列表中 hive 的索引</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>指向 UNICODE_STRING 结构的指针，该结构包含 hive 的文件名</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

无法链接的注册表配置单元可能为 SAM、安全性、软件或默认值。 Hive 有效，因为它已成功加载。

检查参数2，了解无法在注册表树中链接 hive 的原因。 此错误的一个常见原因是 Windows 操作系统的系统驱动器磁盘空间不足。  (在这种情况下，此参数为0xC000017D，状态为 \_ 无 \_ 日志 \_ 空间。 ) 另一个常见问题是尝试分配池失败。  (在这种情况下，参数2为0xC000009A，状态 \_ \_ 资源不足。 ) 必须调查其他状态代码。

 

 




