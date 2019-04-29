---
title: Bug 检查 0x10C FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION
description: FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION bug 检查具有值，该值指示 FsRtl ECP 包中检测到违反 0x0000010C。
ms.assetid: b702b182-696a-4233-8bd0-23a52ab2ddc4
keywords:
- Bug 检查 0x10C FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION
- FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b8d9b15a8c370fa69d76bacb83428d5048aa234
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357621"
---
# <a name="bug-check-0x10c-fsrtlextracreateparameterviolation"></a>Bug 检查 0x10C：FSRTL\_EXTRA\_CREATE\_PARAMETER\_VIOLATION


FSRTL\_额外\_创建\_参数\_冲突错误检查的值为 0x0000010C。 这表示在文件系统运行时库 (FsRtl) 额外创建参数 (ECP) 包中检测到冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="fsrtlextracreateparameterviolation-parameters"></a>FSRTL\_额外\_创建\_参数\_冲突参数


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
<td align="left"><p>冲突的类型。 （请参阅下表更高版本在此页以进行更多详细信息）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>在 ECP 的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ECP 列表的起始地址。</p></td>
</tr>
</tbody>
</table>

 

值为参数 1 指示冲突的类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">类型的冲突</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>ECP 签名无效，由于无效的指针或内存损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>在 ECP 有未定义的标志集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>在 ECP 未通过 FsRtl 进行分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>在 ECP 具有中是非法的用于创建调用方传递的参数的标志集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>在 ECP 已损坏;其大小小于标头大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>正在释放在 ECP 具有非空列表的指针;它仍然可能 ECP 列表的一部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>ECP 列表签名无效，由于无效的指针或内存损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>ECP 列表有未定义的标志集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>通过 FsRtl 未分配 ECP 列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ECP 列表有设置标志，是非法的有关通过创建调用方传递的参数列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>通过创建调用方传递 ECP 列表为空。</p></td>
</tr>
</tbody>
</table>

 

 

 




