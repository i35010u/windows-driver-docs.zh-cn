---
title: logexts. logi
description: Logexts logi 扩展通过将记录器注入到目标应用程序来初始化日志记录。
keywords:
- logexts logi Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3bb9e3d90a276a6cc780509c449ad6561cc79db4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829781"
---
# <a name="logextslogi"></a>!logexts.logi


**！ Logexts logi** 扩展通过将记录器注入目标应用程序来初始化日志记录。

```dbgcmd
    !logexts.logi [OutputDirectory] 
```

## <a name="span-idddk__logexts_logi_dbgspanspan-idddk__logexts_logi_dbgspanparameters"></a><span id="ddk__logexts_logi_dbg"></span><span id="DDK__LOGEXTS_LOGI_DBG"></span>参数


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

此命令初始化日志记录，但并不真正启用日志记录。 可以通过 [**！ logexts. loge**](-logexts-loge.md) 命令启用日志记录。

 

 





