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
ms.openlocfilehash: f1d56451c0849adc9f196cb4c3f6546e3cbb70f1
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025305"
---
# <a name="fileobj"></a>!fileobj


**! Fileobj**扩展显示有关文件\_对象结构的详细信息。

```dbgcmd
!fileobj FileObject
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span>*FileObject*   
指定[FILE_OBJECT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_object)结构的地址。

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

有关文件对象的信息, 请参阅 "Microsoft Windows SDK 文档"、"Windows 驱动程序工具包 (WDK)" 文档和*Microsoft Windows 内部*的 "标记 Russinovich" 和 "David 所罗门群岛"。

<a name="remarks"></a>备注
-------

如果文件\_对象结构有关联的缓存, **! fileobj**将尝试分析并显示缓存信息。

 

 





