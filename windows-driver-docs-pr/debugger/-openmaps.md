---
title: openmaps
description: Openmaps 扩展为指定共享缓存映射显示引用的缓冲区控制块 (BCBs) 和虚拟地址控制块 (VACBs)。
ms.assetid: 4ecce331-c18e-462a-807a-b8929059b897
keywords:
- BCB (缓冲区控制块)
- VACB (虚拟地址控制块)
- 共享缓存映射
- 缓存管理器
- openmaps Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- openmaps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35ed5b7cc429e3bdc2505171b642aad0a7970598
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025201"
---
# <a name="openmaps"></a>!openmaps


**! Openmaps** extension 为指定的共享缓存映射显示引用的缓冲区控制块 (BCBs) 和虚拟地址控制块 (VACBs)。

```dbgcmd
!openmaps Address [Flag]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定共享缓存映射的地址。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span>*标志*   
确定要显示的控制块。 如果*标志*为**1**, 则调试器将显示所有的控制块。 如果*标志*为**0**, 则调试器只显示引用的控制块。 默认值为 **0**。

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
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关缓存管理的信息, Microsoft Windows SDK 请参阅 Russinovich 文档和*Microsoft Windows 内部机制*, 并标记和 David 所罗门群岛。

有关其他缓存管理扩展的信息, 请参阅[ **! cchelp**](-cchelp.md) extension。

 

 





