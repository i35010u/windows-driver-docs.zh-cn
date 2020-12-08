---
title: Bug 检查 0xC0000218 STATUS_CANNOT_LOAD_REGISTRY_FILE
description: STATUS_CANNOT_LOAD_REGISTRY_FILE bug 检查的值为0xC0000218。 这表明无法加载注册表文件。
keywords:
- Bug 检查 0xC0000218 STATUS_CANNOT_LOAD_REGISTRY_FILE
- STATUS_CANNOT_LOAD_REGISTRY_FILE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- STATUS_CANNOT_LOAD_REGISTRY_FILE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c660f8b5885f50dbd86fa4a5b47a473d413138ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783527"
---
# <a name="bug-check-0xc0000218-status_cannot_load_registry_file"></a>Bug 检查0xC0000218：状态 \_ 无法 \_ 加载 \_ 注册表 \_ 文件


状态 \_ 无法 \_ 加载 \_ 注册表 \_ 文件错误检查的值为0xC0000218。 这表明无法加载注册表文件。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="status_cannot_load_registry_file-parameters"></a>状态 \_ 无法 \_ 加载 \_ 注册表 \_ 文件参数


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
<td align="left"><p>无法加载的注册表配置单元的名称的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>零 (保留) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>零 (保留) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>零 (保留) </p></td>
</tr>
</tbody>
</table>

 

此 bug 检查显示描述性文本消息。 损坏文件的名称将显示为消息的一部分。

<a name="cause"></a>原因
-----

如果无法加载必要的注册表配置单元文件，则会发生此错误。 通常，这意味着该文件已损坏或丢失。

在极少数情况下，此错误可能是由损坏了内存中的注册表映像的驱动程序或此区域中的内存错误引起的。

<a name="resolution"></a>解决方法
----------

尝试使用启动恢复机制 (例如，启动修复、恢复控制台或操作系统提供的紧急恢复磁盘) 。 如果问题是注册表文件丢失或损坏，通常会解决此问题。

 

 




