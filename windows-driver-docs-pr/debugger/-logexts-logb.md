---
title: logexts.logb
description: Logexts.logb 扩展显示或刷新输出缓冲区。
ms.assetid: 3c6ec412-f800-469b-9a9f-ebc2940d00fe
keywords:
- logexts.logb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7e3309d55ecfb336e59024e9660dba6c0ff53e32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575497"
---
# <a name="logextslogb"></a>!logexts.logb


**！ Logexts.logb**扩展显示或刷新输出缓冲区。

```dbgcmd
!logexts.logb p 
!logexts.logb f 
```

## <a name="span-idddklogextslogbdbgspanspan-idddklogextslogbdbgspanparameters"></a><span id="ddk__logexts_logb_dbg"></span><span id="DDK__LOGEXTS_LOGB_DBG"></span>参数


<span id="_______p______"></span><span id="_______P______"></span> **p**   
导致要在调试器中显示的输出缓冲区的内容。

<span id="_______f"></span><span id="_______F"></span> **f**  
输出缓冲区刷新到磁盘。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[记录器和日志查看器](logger-and-logviewer.md)。

<a name="remarks"></a>备注
-------

作为性能的考虑因素，日志输出被刷新到磁盘仅当输出缓冲区已满时。 默认情况下，缓冲区为 2144 字节。

**！ Logexts.logb p**扩展在调试器中显示的缓冲区的内容。

**！ Logexts.logb f**扩展缓冲区刷新到日志文件。 因为缓冲区内存由目标应用程序，如果发生访问冲突或某些其他不可恢复的错误，目标应用程序中不会发生自动写入到磁盘的缓冲区。 在这种情况下，应使用此命令以手动刷新到磁盘的缓冲区。 否则，最近日志记录 Api 可能不会显示在日志文件中。

 

 





