---
title: 启用关闭异常
description: 启用关闭异常
keywords:
- '启用 (全局标志的关闭异常) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad437fea5fd7a7b125c11e038a5ff1f808fc163c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834767"
---
# <a name="enable-close-exception"></a>启用关闭异常


## <span id="ddk_enable_close_exception_dtools"></span><span id="DDK_ENABLE_CLOSE_EXCEPTION_DTOOLS"></span>


每当无效的句柄传递到 **CloseHandle** 接口或将句柄作为参数的相关接口（如 **SetEvent**）时， **Enable close exception** 标志将引发用户模式异常。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>ece</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x00400000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_ENABLE_CLOSE_EXCEPTIONS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

**注意**   此标志仍受支持，但是 " [启用错误的句柄检测](enable-bad-handles-detection.md) " 标志 (bhd ") ，这会对句柄使用执行更全面的检查，这是首选选项。

 

 

 





