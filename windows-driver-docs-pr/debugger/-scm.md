---
title: scm
description: Scm 扩展显示指定的共享缓存映射。
ms.assetid: 4333ee14-ca28-43af-b132-210996328af2
keywords:
- 共享缓存映射
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
ms.openlocfilehash: c4ba38a988d1f1ec92b75fbe05db4b17863dc9b9
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025159"
---
# <a name="scm"></a>!scm


**! Scm**扩展显示指定的共享缓存映射。

```dbgcmd
!scm Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定共享缓存映射的地址。

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
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关缓存管理的信息, Microsoft Windows SDK 请参阅 Russinovich 文档和*Microsoft Windows 内部机制*, 并标记和 David 所罗门群岛。

有关其他缓存管理扩展的信息, 请参阅[ **! cchelp**](-cchelp.md) extension。

<a name="remarks"></a>备注
-------

在 Windows XP 和更高版本的 Windows 中, 使用[**dt nt\_ !共享\_缓存\_映射地址**](dt--display-type-.md)命令而不是 **! scm**。

 

 





