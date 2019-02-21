---
title: 启用关闭异常
description: 启用关闭异常
ms.assetid: 4089df14-3204-4a48-b67f-cf6bd53100a5
keywords:
- 启用关闭异常 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47bd62aa61664b6a25b5e15b1badf8e023d03932
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544313"
---
# <a name="enable-close-exception"></a>启用关闭异常


## <span id="ddk_enable_close_exception_dtools"></span><span id="DDK_ENABLE_CLOSE_EXCEPTION_DTOOLS"></span>


**启用关闭异常**标志，则引发用户模式异常时无效的句柄传递给**CloseHandle**接口或相关的接口，如**SetEvent**，需要作为自变量的句柄。

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
<td align="left"><p>整个系统的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

**请注意**  此标志仍受支持，但[启用错误句柄检测](enable-bad-handles-detection.md)标志 (bhd) 执行的句柄使用的更复杂的检查，是首选。

 

 

 





