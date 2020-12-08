---
title: logexts.logd
description: Logexts. logd extension 禁用日志记录。
keywords:
- logexts logd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4b556390affe4e1ba3567ba12394f490adeba4ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829801"
---
# <a name="logextslogd"></a>!logexts.logd


**！ Logexts logd** 扩展禁用日志记录。

```dbgcmd
    !logexts.logd 
```

## <span id="ddk__logexts_logd_dbg"></span><span id="DDK__LOGEXTS_LOGD_DBG"></span>


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

这将导致删除所有 API 挂钩，以使程序可以自由运行。 不会删除 COM 挂钩，因为它们不能在需要时重新启用。

 

 





