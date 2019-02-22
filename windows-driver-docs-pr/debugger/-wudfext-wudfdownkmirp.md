---
title: wudfext.wudfdownkmirp
description: Wudfext.downkmmirp 扩展到指定的用户模式的 I/O 请求数据包 (UM IRP) 中显示内核模式 I/O 请求数据包 (IRP) 相对应。
ms.assetid: f5c42040-2349-4469-a398-12a238ff170e
keywords:
- wudfext.wudfdownkmirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdownkmirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b5ff320dbf704fd8440d8ca943556bc84fdcc4be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554148"
---
# <a name="wudfextwudfdownkmirp"></a>!wudfext.wudfdownkmirp


**！ Wudfext.downkmmirp**扩展到指定的用户模式的 I/O 请求数据包 (UM IRP) 中显示内核模式 I/O 请求数据包 (IRP) 相对应。

```dbgcmd
!wudfext.wudfdownkmirp Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定其相应的内核模式 IRP 将用来显示 UM IRP 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以使用[ **！ wudfext.umirps** ](-wudfext-umirps.md)扩展命令以在主机进程显示所有未完成 UM Irp 的列表。

 

 





