---
title: Bug 检查 0x10C FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION
description: FSRTL_EXTRA_CREATE_PARAMETER_VIOLATION bug 检查的值为0x0000010C，指示在 FsRtl ECP 包中检测到冲突。
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
ms.openlocfilehash: 63493a4be42d018d5fbd927593263c45ac4a00c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790071"
---
# <a name="bug-check-0x10c-fsrtl_extra_create_parameter_violation"></a>Bug 检查0x10C： FSRTL \_ 额外的 \_ CREATE \_ 参数 \_ 冲突


FSRTL \_ 额外的 \_ CREATE \_ PARAMETER \_ 违例 bug 检查的值为0x0000010C。 这表明在文件系统运行时库中检测到冲突 (FsRtl) 额外的 Create 参数 (ECP) 包。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="fsrtl_extra_create_parameter_violation-parameters"></a>FSRTL \_ 额外的 \_ CREATE \_ PARAMETER \_ 违例参数


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
<td align="left"><p>冲突类型。  (查看下表以了解更多详细信息) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>ECP 的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ECP 列表的起始地址。</p></td>
</tr>
</tbody>
</table>

 

参数1的值指示冲突类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">冲突类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>由于错误的指针或内存损坏，ECP 签名无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>ECP 包含未定义的标志集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>FsRtl 未分配 ECP。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>ECP 具有对 create 调用方传递的参数非法的标志集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>ECP 已损坏;其大小小于标头大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>正在释放的 ECP 具有非空的列表指针;它仍可能是 ECP 列表的一部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>由于错误的指针或内存损坏，ECP 列表签名无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>ECP 列表具有未定义的标志集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>FsRtl 未分配 ECP 列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ECP 列表具有对 create 调用方传递的参数列表非法的标志集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>Create 调用方传递的 ECP 列表为空。</p></td>
</tr>
</tbody>
</table>

 

 

 




