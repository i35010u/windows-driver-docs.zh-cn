---
title: cmreslist
description: Cmreslist 扩展显示指定的设备对象的 CM_RESOURCE_LIST 结构。
ms.assetid: 56b48f62-c638-4082-95d7-5a0c62c94212
keywords:
- CM_RESOURCE_LIST
- cmreslist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cmreslist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9e29e703474d75e46e7b6f9b5ec6c657ffbdc059
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334622"
---
# <a name="cmreslist"></a>!cmreslist


**！ Cmreslist**扩展插件都会显示 CM\_资源\_列表结构指定的设备对象。

```dbgsyntax
!cmreslist Address
```

## <a name="span-idddkcmreslistdbgspanspan-idddkcmreslistdbgspanparameters"></a><span id="ddk__cmreslist_dbg"></span><span id="DDK__CMRESLIST_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的十六进制地址的 CM\_资源\_列表结构。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 璝惠 CM\_资源\_列表结构中，请参阅 Windows Driver Kit (WDK) 文档。

 

 





