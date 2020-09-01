---
title: mapped_file
description: Mapped_file 扩展显示文件映射的文件名称，该文件映射包含指定的地址。
ms.assetid: 1d6d4d14-01ca-47ce-a044-778c9a56e9a5
keywords:
- mapped_file Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- mapped_file
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 577d87c98432bcbfb2b1a712b2a5f108876ad489
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212623"
---
# <a name="mapped_file"></a>！映射 \_ 文件


**！映射的 \_ 文件**扩展名显示文件映射的文件的名称，该文件映射包含指定的地址。

```dbgcmd
!mapped_file Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定文件映射的地址。 如果 *地址* 不在映射中，则该命令将失败。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

**！映射的 \_ 文件**扩展名只能在实时 nonremote 调试过程中使用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关文件映射的详细信息，请参阅 Windows SDK 中的 [MapViewOfFile](/windows/win32/api/memoryapi/nf-memoryapi-mapviewoffile) 。

<a name="remarks"></a>备注
-------

下面是三个示例。 使用的前两个地址是从文件中映射的，而第三个地址则不是。

```dbgcmd
0:000> !mapped_file 4121ec 
Mapped file name for 004121ec: '\Device\HarddiskVolume2\CODE\TimeTest\Debug\TimeTest.exe'

0:000> !mapped_file 77150000 
Mapped file name for 77150000: '\Device\HarddiskVolume2\Windows\System32\kernel32.dll'

0:000> !mapped_file 80310000 
No information found for 80310000: error 87
```

 

