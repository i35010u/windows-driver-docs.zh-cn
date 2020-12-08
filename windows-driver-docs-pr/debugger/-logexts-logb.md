---
title: logexts. logb
description: Logexts. logb 扩展显示或刷新输出缓冲区。
keywords:
- logexts logb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 34ead337a280ca7e91c1e882b27fdf8160dc5fa0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829803"
---
# <a name="logextslogb"></a>!logexts.logb


**！ Logexts logb** 扩展显示或刷新输出缓冲区。

```dbgcmd
!logexts.logb p 
!logexts.logb f 
```

## <a name="span-idddk__logexts_logb_dbgspanspan-idddk__logexts_logb_dbgspanparameters"></a><span id="ddk__logexts_logb_dbg"></span><span id="DDK__LOGEXTS_LOGB_DBG"></span>参数


<span id="_______p______"></span><span id="_______P______"></span>**p**   
使输出缓冲区的内容显示在调试器中。

<span id="_______f"></span><span id="_______F"></span>**f**  
将输出缓冲区刷新到磁盘。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [记录器和 LogViewer](logger-and-logviewer.md)。

<a name="remarks"></a>备注
-------

作为性能方面的考虑，仅当输出缓冲区已满时才将日志输出刷新到磁盘。 默认情况下，缓冲区为2144字节。

**！ Logexts; logb p** 扩展在调试器中显示缓冲区的内容。

**！ Logexts logb f** extension 将缓冲区刷新到日志文件。 由于缓冲区内存由目标应用程序管理，因此，如果在目标应用程序中出现访问冲突或其他无法恢复的错误，则不会自动将缓冲区写入磁盘。 在这种情况下，应使用此命令手动将缓冲区刷新到磁盘。 否则，最新记录的 Api 可能不会出现在日志文件中。

 

 





