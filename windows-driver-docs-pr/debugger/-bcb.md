---
title: bcb
description: Bcb 扩展显示指定的缓冲区控制块。
keywords:
- 缓存管理器
- bcb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bcb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f426d89f1b2ee0a71c5d8422a683066a36d61506
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799993"
---
# <a name="bcb"></a>!bcb


**！ Bcb** 扩展显示指定的缓冲区控制块。

```dbgcmd
!bcb Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定缓冲区控制块的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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
<td align="left"><p> (，请参阅 "备注" 部分) </p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关缓存管理的信息，Microsoft Windows SDK 请参阅 Russinovich 文档和 *Microsoft Windows 内部机制* ，并标记和 David 所罗门群岛。

有关其他缓存管理扩展的信息，请使用 [**！ cchelp**](-cchelp.md) 扩展。

<a name="remarks"></a>备注
-------

此扩展仅适用于 Windows 2000。 在 Windows XP 或更高版本中，使用 [**dt nt！ \_BCB Address**](dt--display-type-.md) 命令可直接显示缓冲区控制块。

 

 





