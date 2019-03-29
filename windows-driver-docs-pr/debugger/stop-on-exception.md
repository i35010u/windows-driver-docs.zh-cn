---
title: 异常时停止
description: 异常时停止
ms.assetid: f459fa28-2fdf-4094-ba58-7e01a2309bb7
keywords:
- 停止的异常 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b79223fdaa80d7417e82089e8449ddb63b5bf546
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568710"
---
# <a name="stop-on-exception"></a>异常时停止


## <span id="ddk_stop_on_exception_dtools"></span><span id="DDK_STOP_ON_EXCEPTION_DTOOLS"></span>


**异常停止**标志会导致进入内核调试器，每次内核模式异常发生时的内核。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>soe</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_STOP_ON_EXCEPTION</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

Windows 将传递所有第一机会异常 (除状态\_端口\_断开连接) 到调试器，然后将其传递给本地异常处理程序在严重级别为警告或错误。

 

 





