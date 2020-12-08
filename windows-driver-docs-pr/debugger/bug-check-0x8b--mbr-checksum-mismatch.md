---
title: Bug 检查 0x8B MBR_CHECKSUM_MISMATCH
description: MBR_CHECKSUM_MISMATCH bug 检查的值为0x0000008B。 此 bug 检查表明 MBR 校验和中出现不匹配。
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
ms.openlocfilehash: 754deb1a5f670a4205921491098ebd5cfd9a23ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819885"
---
# <a name="bug-check-0x8b-mbr_checksum_mismatch"></a>Bug 检查0x8B： MBR \_ 校验和 \_ 不匹配


MBR \_ 校验和 \_ bug 检查的值为0x0000008B。 此 bug 检查表明 MBR 校验和中出现不匹配。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="mbr_checksum_mismatch-parameters"></a>MBR \_ 校验和 \_ 不匹配参数


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
<td align="left"><p>MBR 的磁盘签名</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>操作系统加载器计算的 MBR 校验和</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>系统计算的 MBR 校验和</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

\_ \_ 当 Microsoft Windows 操作系统计算的 mbr 校验和与加载器传入的校验和不匹配时，在启动过程中将发生 mbr 校验和不匹配 bug 检查。

此错误通常表示病毒。

<a name="resolution"></a>解决方法
----------

可以检测到多种形式的病毒，而不能检测到所有病毒。 通常，较新病毒通常只能由最近升级的病毒扫描程序检测到。 应使用包含病毒扫描程序的写保护磁盘启动，并尝试清除感染。

 

 




