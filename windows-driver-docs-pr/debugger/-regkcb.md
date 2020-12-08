---
title: regkcb
description: Regkcb 扩展显示注册表项控制块。
keywords:
- regkcb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- regkcb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9cf68e375ed51aceaf8e1b37d939fd05b494cede
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795219"
---
# <a name="regkcb"></a>!regkcb


**！ Regkcb** extension 显示注册表项控制块。

```dbgcmd
!regkcb Address 
```

## <a name="span-idddk__regkcb_dbgspanspan-idddk__regkcb_dbgspanparameters"></a><span id="ddk__regkcb_dbg"></span><span id="DDK__REGKCB_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定密钥控制块的地址。

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
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关注册表及其组件的信息，请参阅 *Microsoft Windows 内部机制*，方法是标记 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

在 Windows 2000 中， **！ regkcb** 显示特定的注册表项控制块。

在 Windows XP 和更高版本的 Windows 中，应改为使用 [**！ reg**](-reg.md) 扩展命令。

每个注册表项都有一个包含属性（如其权限）的控制块。

 

 





