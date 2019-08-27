---
title: pcm
description: Pcm 扩展显示指定的专用缓存映射。 此扩展仅在 Windows 2000 中提供。
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
ms.openlocfilehash: f1c151f67bfdc65d9e8e3abc2f08939b8f745b9a
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025199"
---
# <a name="pcm"></a>!pcm


**! Pcm**扩展显示指定的专用缓存映射。 此扩展仅在 Windows 2000 中提供。

```dbgcmd
!pcm Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定专用缓存映射的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>不可用 (请参阅 "备注" 部分)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关缓存管理的信息, Microsoft Windows SDK 请参阅 Russinovich 文档和*Microsoft Windows 内部机制*, 并标记和 David 所罗门群岛。

有关其他缓存管理扩展的信息, 请参阅[ **! cchelp**](-cchelp.md) extension reference。

<a name="remarks"></a>备注
-------

只有 Windows 2000 支持此扩展。 在 Windows XP 和更高版本的 Windows 中, 使用[**dt nt\_ !专用\_缓存\_映射地址**](dt--display-type-.md)命令。

 

 





