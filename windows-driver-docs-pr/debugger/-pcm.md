---
title: pcm
description: Pcm 扩展将显示指定的专用缓存地图。 此扩展才可用在 Windows 2000 中。
ms.assetid: a6880ad0-5326-4bea-ac84-3311a2ec01da
keywords:
- 专用缓存映射
- 缓存管理器
- pcm Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1ede535bc8316dc8e5cb0e4c2ad37a5dcf3b9631
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334414"
---
# <a name="pcm"></a>!pcm


**！ Pcm**扩展显示指定的专用缓存映射。 此扩展才可用在 Windows 2000 中。

```dbgcmd
!pcm Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定专用缓存映射的地址。

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
<td align="left"><p>不可用 (请参阅备注部分)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

缓存管理有关的信息，请参阅 Microsoft Windows SDK 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

有关其他缓存管理扩展的信息，请参阅[ **！ cchelp** ](-cchelp.md)扩展引用。

<a name="remarks"></a>备注
-------

仅在 Windows 2000 中支持此扩展。 在 Windows XP 和更高版本的 Windows 中，使用[ **dt nt ！\_私有\_缓存\_映射地址**](dt--display-type-.md)命令。

 

 





