---
title: Bug Check 0x14A KERNEL_WMI_INTERNAL
description: KERNEL_WMI_INTERNAL bug 检查具有 0x0000014A 值。 这表示内部内核 WMI 子系统遇到致命错误。
ms.assetid: 2E739F6B-4618-44A5-B060-F2BCB77B82A3
keywords:
- Bug Check 0x14A KERNEL_WMI_INTERNAL
- KERNEL_WMI_INTERNAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_WMI_INTERNAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4a85749a4909b28da9920469bd65521237c1f95e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521212"
---
# <a name="bug-check-0x14a-kernelwmiinternal"></a>Bug 检查 0x14A:KERNEL\_WMI\_INTERNAL


内核\_WMI\_内部 bug 检查的值为 0x0000014A。 这表示内部内核 WMI 子系统遇到致命错误。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="kernelwmiinternal-parameters"></a>内核\_WMI\_内部参数


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
<td align="left">1</td>
<td align="left"><p>0 :从 0 增加了内核 WMI 条目引用计数。</p>
参数 2:内核 WMI 条目的指针。
<p>1 :内核 WMI 数据源已过早删除。</p>
参数 2:到内核 WMI 数据源的指针。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">保留</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

 

 




