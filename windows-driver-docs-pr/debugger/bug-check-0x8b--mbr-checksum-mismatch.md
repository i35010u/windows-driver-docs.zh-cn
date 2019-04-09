---
title: Bug 检查 0x8B MBR_CHECKSUM_MISMATCH
description: MBR_CHECKSUM_MISMATCH bug 检查具有 0x0000008B 值。 此 bug 检查指示 MBR 校验和中出现不匹配。
ms.assetid: 7db57605-b6ff-49b9-8a79-3325512825b9
keywords:
- Bug 检查 0x8B MBR_CHECKSUM_MISMATCH
- MBR_CHECKSUM_MISMATCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MBR_CHECKSUM_MISMATCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b0aa37b409a9a4212f94fe1fc117bbb73c5b991
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238450"
---
# <a name="bug-check-0x8b-mbrchecksummismatch"></a>Bug 检查 0x8B：MBR\_校验和\_不匹配


MBR\_校验和\_不匹配错误检查的值为 0x0000008B。 此 bug 检查指示 MBR 校验和中出现不匹配。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="mbrchecksummismatch-parameters"></a>MBR\_校验和\_不匹配参数


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
<td align="left"><p>从 MBR 磁盘签名</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>操作系统加载程序计算 MBR 校验和</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>系统会计算 MBR 校验和</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

MBR\_校验和\_启动过程中发生的不匹配错误检查，Microsoft Windows 操作系统计算的 MBR 校验和与加载程序将传入的校验和不匹配时。

此错误通常指示病毒。

<a name="resolution"></a>分辨率
----------

有许多形式的病毒，可以检测到不是全部。 通常情况下，较新的病毒通常可以检测到只能由最近升级了病毒扫描程序。 应使用受写保护的磁盘包含病毒扫描程序启动并尝试清除感染。

 

 




