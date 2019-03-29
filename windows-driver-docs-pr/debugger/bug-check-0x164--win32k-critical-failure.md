---
title: Bug 检查 0x164 WIN32K_CRITICAL_FAILURE
description: WIN32K_CRITICAL_FAILURE bug 检查具有 0x00000164 值。 这指示 Win32k 遇到严重故障。
ms.assetid: 6274C852-53DA-4E01-B2A6-D7485501BE50
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
ms.openlocfilehash: ccde555cee1569001d053652d654a43284fd12e5
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464371"
---
# <a name="bug-check-0x164-win32kcriticalfailure"></a>Bug 检查 0x164：WIN32K\_严重\_失败


WIN32K\_严重\_故障错误检查的值为 0x00000164。 这指示 Win32k 遇到严重故障。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="win32kcriticalfailure-parameters"></a>WIN32K\_严重\_失败参数


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
0x1:REGION_VALIDATION_FAILURE 的区域是超出图面上的界限。
<p>2-指向 DC</p>
<p>3-到图面指针</p>
<p>4-指向区域</p>
0x2:OPERATOR_NEW_USED-"new"运算符用于分配内存。
<p>2-保留</p>
<p>3-保留</p>
<p>4-保留</p>
<p></p>
0x3:CRITICAL_APISET_EXTENSIONS_MISSING-关键扩展 APISET API 缺少。
<p>2-wchar_t * 到缺失函数的名称</p>
<p>3-保留</p>
<p>4-保留</p>
0x4:GDI_SPRITE_SURFACE_INVALID_DELETE-正在删除而不删除子画面 GDI sprite 的形状。
<p>2-句柄在图面</p>
<p>3-引用计数到图面</p>
<p>4-PID 的图面上的所有者</p>
0x5:POINTER_DEVICE_EXCLUSIVE_OPEN_FAILED-无法打开指针设备。
<p></p>
<p>2-UNICODE_STRING 的设备</p>
<p>3-保留</p>
<p>4-保留</p>
0x8:PUBLIC_DC_INVALID_PRIVATE_MEMBER-公共 DC 具有指向特定的进程所拥有的对象的指针。
<p>2-指向 DC</p>
<p>3-拥有此对象的进程 id</p>
<p>4-保留</p>
0xA:在 TTFD 中正在使用 TTFD_INVOKE_ILLEGAL_ID-无效的函数表索引。
<p>2-保留</p>
<p>3-保留</p>
<p>4-保留</p>
0xB:在 ATMFD 中正在使用 OTFD_INVOKE_ILLEGAL_ID-无效的函数表索引。
<p>2-保留</p>
<p>3-保留</p>
<p>4-保留</p>
0xC:在调色板中正在使用 GFPE_INVOKE_ILLEGAL_ID-无效的函数表索引。
<p>2-指向调色板</p>
<p>3-无效的索引</p>
<p>4-最大有效索引 + 1</p>
0x10:USER_SAS_REGISTRATION_FAILED-SAS 密钥注册已失败。
<p>2-vkey</p>
<p>3-修饰符</p>
<p>4-标志</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数 1</td>
</tr>
</tbody>
</table>

 

 

 




