---
title: mapped_file
description: Mapped_file 扩展显示将包含指定的地址的文件映射的文件的名称。
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
ms.openlocfilehash: 8a38e66b023c84fa72123bcd6d1f88908f8fc461
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336113"
---
# <a name="mappedfile"></a>!mapped\_file


**！ 映射\_文件**扩展显示将包含指定的地址的文件映射的文件的名称。

```dbgcmd
!mapped_file Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的文件映射的地址。 如果*地址*不在映射中，该命令将失败。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

**！ 映射\_文件**扩展仅可实时、 可 nonremote 调试期间使用。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关文件映射的详细信息，请参阅[MapViewOfFile](https://go.microsoft.com/fwlink/p/?linkid=123354) Windows SDK 中。

<a name="remarks"></a>备注
-------

以下是三个示例。 使用的前两个地址将映射从一个文件，并不是第三个。

```dbgcmd
0:000> !mapped_file 4121ec 
Mapped file name for 004121ec: '\Device\HarddiskVolume2\CODE\TimeTest\Debug\TimeTest.exe'

0:000> !mapped_file 77150000 
Mapped file name for 77150000: '\Device\HarddiskVolume2\Windows\System32\kernel32.dll'

0:000> !mapped_file 80310000 
No information found for 80310000: error 87
```

 

 





