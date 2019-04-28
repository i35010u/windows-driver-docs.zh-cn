---
title: logexts.logi
description: Logexts.logi 扩展通过将记录器注入到目标应用程序初始化日志记录。
ms.assetid: c02d2799-c83a-455d-90c0-401244062365
keywords:
- logexts.logi Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 45875b0a663aeb83581401216469f04e57bdc800
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336151"
---
# <a name="logextslogi"></a>!logexts.logi


**！ Logexts.logi**扩展通过将记录器注入到目标应用程序初始化日志记录。

```dbgcmd
    !logexts.logi [OutputDirectory] 
```

## <a name="span-idddklogextslogidbgspanspan-idddklogextslogidbgspanparameters"></a><span id="ddk__logexts_logi_dbg"></span><span id="DDK__LOGEXTS_LOGI_DBG"></span>参数


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

此命令初始化日志记录，但不会实际启用它。 可以使用启用日志记录[ **！ logexts.loge** ](-logexts-loge.md)命令。

 

 





