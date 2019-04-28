---
title: logexts.logd
description: Logexts.logd 扩展禁用日志记录。
ms.assetid: d3c3403d-f86b-4f2a-a261-c00eb0b2b756
keywords:
- logexts.logd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1ee01792b89f84b6e777337e842425fb32f01b69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336134"
---
# <a name="logextslogd"></a>!logexts.logd


**！ Logexts.logd**扩展禁用日志记录。

```dbgcmd
    !logexts.logd 
```

## <span id="ddk__logexts_logd_dbg"></span><span id="DDK__LOGEXTS_LOGD_DBG"></span>


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

这将导致所有 API 挂钩，为了允许自由地运行应用程序中删除。 COM 挂钩不会删除，因为它们不能在重新启用。

 

 





