---
title: logexts.loge
description: Logexts.loge 扩展启用日志记录。 如果尚未初始化日志记录，它将初始化并启用。
ms.assetid: d8b621f1-19e7-4c42-a428-8572d29b666f
keywords:
- logexts.loge Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.loge
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25d2760977acb60e7351473100a21b3061e4dc80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575388"
---
# <a name="logextsloge"></a>!logexts.loge


**！ Logexts.loge**扩展启用日志记录。 如果尚未初始化日志记录，它将初始化并启用。

```dbgcmd
    !logexts.loge [OutputDirectory] 
```

## <a name="span-idddklogextslogedbgspanspan-idddklogextslogedbgspanparameters"></a><span id="ddk__logexts_loge_dbg"></span><span id="DDK__LOGEXTS_LOGE_DBG"></span>参数


<span id="_______OutputDirectory______"></span><span id="_______outputdirectory______"></span><span id="_______OUTPUTDIRECTORY______"></span> *OutputDirectory*   
指定要用于输出的目录。 如果*OutputDirectory*指定，则它必须存在-调试器不会创建它。 如果指定了相对路径，则它将相对于从中启动调试器的目录。 如果*OutputDirectory*是省略，就会使用到桌面的路径。 调试器将创建的 LogExts 子目录*OutputDirectory*，并将所有记录器输出将都置于此子目录。

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

如果记录器未尚未已插入到目标应用程序通过[ **！ logexts.logi** ](-logexts-logi.md)扩展 **！ logexts.loge**扩展将注入到目标的记录器和然后，启用日志记录。

如果[ **！ logexts.logi** ](-logexts-logi.md)并且尚未运行，不能包括*OutputDirectory*，因为输出目录将已设置。

 

 





