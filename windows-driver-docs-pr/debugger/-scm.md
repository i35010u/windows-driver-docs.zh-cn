---
title: scm
description: Scm 扩展将显示指定的共享的缓存地图。
ms.assetid: 4333ee14-ca28-43af-b132-210996328af2
keywords:
- 共享的缓存映射
- 缓存管理器
- scm Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- scm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58a985eb874522ff9289b0b038211fec30b7d3b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330786"
---
# <a name="scm"></a>!scm


**！ Scm**扩展显示指定的共享的缓存映射。

```dbgcmd
!scm Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定共享的缓存映射的地址。

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
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

缓存管理有关的信息，请参阅 Microsoft Windows SDK 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

有关其他缓存管理扩展的信息，请参阅[ **！ cchelp** ](-cchelp.md)扩展。

<a name="remarks"></a>备注
-------

在 Windows XP 和更高版本的 Windows 中，使用[ **dt nt ！\_共享\_缓存\_映射地址**](dt--display-type-.md)命令而不是 **！ scm**。

 

 





