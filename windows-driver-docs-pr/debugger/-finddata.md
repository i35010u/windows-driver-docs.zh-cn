---
title: finddata
description: Finddata 扩展显示按指定的文件对象中给定的偏移量的缓存的数据。
ms.assetid: 1d6f920b-5716-4ccc-8c2d-08b422f57124
keywords:
- 缓存管理器
- finddata Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- finddata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e001a16ddf155d32d0e8923572b34a4af7b87729
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575473"
---
# <a name="finddata"></a>!finddata


**！ Finddata**扩展缓存的数据显示在指定的文件对象中给定的偏移量。

```dbgcmd
!finddata FileObject Offset
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span> *FileObject*   
指定的文件对象的地址。

<span id="_______Offset______"></span><span id="_______offset______"></span><span id="_______OFFSET______"></span> *Offset*   
指定的偏移量。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

缓存管理有关的信息，请参阅 Microsoft Windows SDK 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

有关其他缓存管理扩展的信息，请参阅[ **！ cchelp** ](-cchelp.md)扩展。

 

 





