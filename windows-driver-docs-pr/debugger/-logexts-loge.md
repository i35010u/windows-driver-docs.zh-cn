---
title: logexts.loge
description: Logexts. loge 扩展启用日志记录。 如果日志记录尚未初始化，则将初始化并启用日志记录。
keywords:
- logexts loge Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.loge
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e356b46861f806ce3f77f30bf679fef7e7eb1b3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829791"
---
# <a name="logextsloge"></a>!logexts.loge


**！ Logexts loge** 扩展启用日志记录。 如果日志记录尚未初始化，则将初始化并启用日志记录。

```dbgcmd
    !logexts.loge [OutputDirectory] 
```

## <a name="span-idddk__logexts_loge_dbgspanspan-idddk__logexts_loge_dbgspanparameters"></a><span id="ddk__logexts_loge_dbg"></span><span id="DDK__LOGEXTS_LOGE_DBG"></span>参数


<span id="_______OutputDirectory______"></span><span id="_______outputdirectory______"></span><span id="_______OUTPUTDIRECTORY______"></span>*OutputDirectory*   
指定要用于输出的目录。 如果指定了 *OutputDirectory* ，则它必须存在--调试器将不会创建它。 如果指定了相对路径，则该路径将是相对于启动调试器的目录的相对路径。 如果省略 *OutputDirectory* ，则使用桌面路径。 调试器将创建 *OutputDirectory* 的 LogExts 子目录，并将所有记录器输出放置在此子目录中。

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

如果已通过 [**！ logexts**](-logexts-logi.md) 将记录器注入到目标应用程序中，则 **！ logexts. loge** 扩展会将记录器注入目标，并启用日志记录。

如果已运行 [**！ logexts**](-logexts-logi.md) ，则不能包含 *OutputDirectory*，因为输出目录已设置。

 

 





