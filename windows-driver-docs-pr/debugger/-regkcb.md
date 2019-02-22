---
title: regkcb
description: Regkcb 扩展显示注册表键控制块。
ms.assetid: d6898025-9ba2-4b3b-819b-d7b23d8ee525
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
ms.openlocfilehash: d775c6c0caa7826c8a81dd198c0bf2f9e14be128
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555486"
---
# <a name="regkcb"></a>!regkcb


**！ Regkcb**扩展，将显示注册表键控制块。

```dbgcmd
!regkcb Address 
```

## <a name="span-idddkregkcbdbgspanspan-idddkregkcbdbgspanparameters"></a><span id="ddk__regkcb_dbg"></span><span id="DDK__REGKCB_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定密钥的控制块的地址。

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

有关注册表及如何及其组件的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

<a name="remarks"></a>备注
-------

在 Windows 2000 中， **！ regkcb**显示特定的注册表密钥控制块。

在 Windows XP 和更高版本的 Windows， [ **！ reg** ](-reg.md)应改为使用扩展命令。

每个注册表项已包含属性，例如其权限的控制块。

 

 





