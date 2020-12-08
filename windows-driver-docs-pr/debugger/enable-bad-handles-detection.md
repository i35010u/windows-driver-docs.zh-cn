---
title: 启用错误句柄检测
description: 启用错误句柄检测
keywords:
- " (全局标志启用错误的句柄检测) "
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41bf4fbc5c8e6d332efcd407f89e6a6382954fbb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834769"
---
# <a name="enable-bad-handles-detection"></a>启用错误句柄检测


## <span id="ddk_enable_bad_handles_detection_dtools"></span><span id="DDK_ENABLE_BAD_HANDLES_DETECTION_DTOOLS"></span>


**Enable bad handles detection** \_ \_ 每当用户模式进程向对象管理器传递无效的句柄时，"启用错误的句柄" 检测标志将引发用户模式异常 (状态无效的句柄) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>bhd</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x40000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_ENABLE_HANDLE_EXCEPTIONS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

 

 





