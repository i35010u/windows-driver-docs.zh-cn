---
title: fileobj
description: Fileobj 扩展显示有关 FILE_OBJECT 结构的详细信息。
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
ms.openlocfilehash: 2774e4758d76d7f907f72daad01f193f71e49f41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826746"
---
# <a name="fileobj"></a>!fileobj


**！ Fileobj**扩展显示有关文件\_对象结构的详细信息。

```dbgcmd
!fileobj FileObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span>*FileObject*   
指定[FILE_OBJECT](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)结构的地址。

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
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关文件对象的信息，请参阅 "Microsoft Windows SDK 文档"、"Windows 驱动程序工具包（WDK）" 文档和*Microsoft Windows 内部*的 "标记 Russinovich" 和 "David 所罗门群岛"。

<a name="remarks"></a>备注
-------

如果\_对象结构的文件具有关联的缓存， **！ fileobj**将尝试分析并显示缓存信息。

 

 





