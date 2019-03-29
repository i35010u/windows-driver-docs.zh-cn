---
title: Bug 检查 0x73 CONFIG_LIST_FAILED
description: CONFIG_LIST_FAILED bug 检查具有 0x00000073 值。 此 bug 检查指示不能在注册表树链接顶级注册表项，也称为核心系统配置单元，其中一个。
ms.assetid: fec1f3ee-5405-49c2-8082-75adfdabd6b8
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
ms.openlocfilehash: ccad585ecc3fcc916a4f8fb3849ee2620e0b28e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576357"
---
# <a name="bug-check-0x73-configlistfailed"></a>Bug 检查 0x73：CONFIG\_列表\_失败


在配置\_列表\_失败错误检查的值为 0x00000073。 此 bug 检查指示不能在注册表树链接顶级注册表项，也称为核心系统配置单元，其中一个。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="configlistfailed-parameters"></a>CONFIG\_列表\_失败参数


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
<td align="left"><p>导致要假定它未能加载配置单元的 Windows 操作系统 NT 状态代码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>配置单元列表中的配置单元的索引</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>指向包含该配置单元文件名称的 UNICODE_STRING 结构的指针</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

不能关联的注册表配置单元可能 SAM、 安全性、 软件或默认值。 该配置单元无效，因为它已成功加载。

检查参数 2，若要查看无法进行 hive 链接在注册表树中。 此错误的一个常见原因是 Windows 操作系统的系统驱动器上的磁盘空间不足。 (在这种情况下，此参数是 0xC000017D，状态\_否\_日志\_空间。)另一个常见问题是分配池的尝试已失败。 (在此情况下，参数 2 是 0xC000009A，状态\_不足\_资源。)您必须先调查其他状态代码。

 

 




