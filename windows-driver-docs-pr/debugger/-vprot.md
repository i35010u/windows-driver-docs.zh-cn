---
title: vprot
description: Vprot 扩展显示虚拟内存保护信息。
ms.assetid: 7ee863ef-abfd-4ee7-9bac-34472e60f3fa
keywords:
- 内存，内存保护
- vprot Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vprot
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b361b4e7c5c9c384c7310cba599acde22419e52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341799"
---
# <a name="vprot"></a>!vprot


**！ Vprot**扩展显示虚拟内存保护信息。

```dbgcmd
!vprot [Address]
```

## <a name="span-idddkvprotdbgspanspan-idddkvprotdbgspanparameters"></a><span id="ddk__vprot_dbg"></span><span id="DDK__VPROT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的内存保护状态将显示的十六进制地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Uext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

若要查看所有拥有的目标进程的内存范围的内存保护信息，请使用[ **！ vadump**](-vadump.md)。 有关内存保护的信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 

<a name="remarks"></a>备注
-------

**！ Vprot**扩展命令可用于实时调试和转储文件调试。

下面是一个示例：

```dbgcmd
0:000> !vprot 30c191c
BaseAddress: 030c1000
AllocationBase: 030c0000
AllocationProtect: 00000080 PAGE_EXECUTE_WRITECOPY
RegionSize: 00011000
State: 00001000 MEM_COMMIT
Protect: 00000010 PAGE_EXECUTE
Type: 01000000 MEM_IMAGE
```

在此显示中 AllocationProtect 行显示的默认保护整个区域用创建。 请注意，此区域内的各个地址可以有分配内存后更改其保护 (例如，如果**VirtualProtect**称为)。 保护线显示为此特定地址实际的保护。 可能的保护的值为页面\_NOACCESS，页面\_READONLY，页面\_READWRITE，页面\_EXECUTE，页\_EXECUTE\_读取、 页\_EXECUTE\_读写页面\_WRITECOPY，页\_EXECUTE\_WRITECOPY 和页\_防护。

状态行还适用于特定的虚拟地址传递给 **！ vprot**。 可能的状态的值为内存优化\_提交、 内存优化\_免费版和内存优化\_保留。

类型行显示的内存类型。 可能的值为内存优化\_图像、 内存优化\_映射，以及内存优化\_专用。

 

 





