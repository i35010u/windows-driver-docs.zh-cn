---
title: wudfext.wudfdownkmirp
description: Downkmmirp 扩展显示 (IRP) 的内核模式 i/o 请求包，它与指定的用户模式 i/o 请求数据包 (UM IRP) 相对应。
keywords:
- wudfext wudfdownkmirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdownkmirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b790f1555543712fa6bb5f51069270d8a87970b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794081"
---
# <a name="wudfextwudfdownkmirp"></a>!wudfext.wudfdownkmirp


**！ Wudfext downkmmirp** 扩展显示与指定用户模式 i/o 请求数据包 (UM IRP) 对应的内核模式 i/o 请求数据包 (IRP) 。

```dbgcmd
!wudfext.wudfdownkmirp Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定将显示其对应内核模式 IRP 的 UM IRP 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

你可以使用 [**！ wudfext umirps**](-wudfext-umirps.md) 扩展命令显示主机进程中所有未完成的 UM irp 的列表。

 

 





