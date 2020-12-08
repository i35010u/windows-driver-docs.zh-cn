---
title: Bug 检查 0x164 WIN32K_CRITICAL_FAILURE
description: WIN32K_CRITICAL_FAILURE bug 检查的值为0x00000164。 这表明 Win32k.sys 遇到了严重故障。
keywords:
- Bug 检查 0x164 WIN32K_CRITICAL_FAILURE
- WIN32K_CRITICAL_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WIN32K_CRITICAL_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 504f4a467cb2dbcb6b18289c4bc009c785d99a88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838533"
---
# <a name="bug-check-0x164-win32k_critical_failure"></a>Bug 检查0x164： WIN32K.SYS \_ 严重 \_ 故障


WIN32K.SYS \_ 严重 \_ 故障 bug 检查的值为0x00000164。 这表明 Win32k.sys 遇到了严重故障。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="win32k_critical_failure-parameters"></a>WIN32K.SYS \_ 严重 \_ 故障参数


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
<td align="left"><p>1-失败的类型。</p>
0x1： REGION_VALIDATION_FAILURE 区域超出了表面界限。
<p>2-指向 DC 的指针</p>
<p>3-指向图面的指针</p>
<p>4-指向区域的指针</p>
0x2： OPERATOR_NEW_USED 运算符 "NEW" 用于分配内存。
<p>2-保留</p>
<p>3-保留</p>
<p>4-保留</p>
<p></p>
0x3：缺少 CRITICAL_APISET_EXTENSIONS_MISSING 关键扩展 APISET API。
<p>2-wchar_t * 到缺少的函数的名称</p>
<p>3-保留</p>
<p>4-保留</p>
0x4 GDI_SPRITE_SURFACE_INVALID_DELETE：正在删除 GDI 动画的形状，但不删除子画面。
<p>图面的2句柄</p>
<p>3-图面的引用计数</p>
<p>4-面的所有者 PID</p>
0x5： POINTER_DEVICE_EXCLUSIVE_OPEN_FAILED 打开指针设备失败。
<p></p>
<p>2-设备 UNICODE_STRING</p>
<p>3-保留</p>
<p>4-保留</p>
0x8： PUBLIC_DC_INVALID_PRIVATE_MEMBER-公共 DC 具有指向特定进程所拥有的对象的指针。
<p>2-指向 DC 的指针</p>
<p>3-拥有对象的进程 id</p>
<p>4-保留</p>
0xA： TTFD_INVOKE_ILLEGAL_ID-TTFD 中使用的函数表索引无效。
<p>2-保留</p>
<p>3-保留</p>
<p>4-保留</p>
0xB： OTFD_INVOKE_ILLEGAL_ID-ATMFD 中使用的函数表索引无效。
<p>2-保留</p>
<p>3-保留</p>
<p>4-保留</p>
0xC： GFPE_INVOKE_ILLEGAL_ID-在调色板中使用的函数表索引无效。
<p>2-指向调色板的指针</p>
<p>3-无效索引</p>
<p>4-最大有效索引 + 1</p>
0x10： USER_SAS_REGISTRATION_FAILED SAS 密钥注册失败。
<p>2-vkey</p>
<p>3-修饰符</p>
<p>4-标志</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数1</td>
</tr>
</tbody>
</table>

 

 

 




