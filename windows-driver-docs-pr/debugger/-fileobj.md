---
title: fileobj
description: Fileobj 扩展显示有关 FILE_OBJECT 结构的详细的信息。
ms.assetid: ee9237e7-8a1f-473c-9e30-f2b0731a7519
keywords:
- FILE_OBJECT
- fileobj Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- fileobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 501553384979186db955d6278edad6c32234dce5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336734"
---
# <a name="fileobj"></a>!fileobj


**！ Fileobj**扩展插件都会显示有关文件的详细的信息\_对象结构。

```dbgcmd
!fileobj FileObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span> *FileObject*   
指定的地址[FILE_OBJECT](https://msdn.microsoft.com/library/windows/hardware/ff545834)结构。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关文件对象的信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

如果该文件\_对象结构有一个关联的缓存 **！ fileobj**尝试分析并显示缓存信息...

 

 





