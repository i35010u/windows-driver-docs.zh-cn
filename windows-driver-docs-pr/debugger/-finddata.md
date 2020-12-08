---
title: finddata
description: Finddata 扩展在指定的文件对象内按给定的偏移量显示缓存的数据。
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
ms.openlocfilehash: 0cf8eddf076903dd53cec4068450c757219a093c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821693"
---
# <a name="finddata"></a>!finddata


**！ Finddata** extension 在指定的文件对象内按给定的偏移量显示缓存的数据。

```dbgcmd
!finddata FileObject Offset
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______FileObject______"></span><span id="_______fileobject______"></span><span id="_______FILEOBJECT______"></span>*FileObject*   
指定文件对象的地址。

<span id="_______Offset______"></span><span id="_______offset______"></span><span id="_______OFFSET______"></span>*偏移量*   
指定偏移量。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关缓存管理的信息，Microsoft Windows SDK 请参阅 Russinovich 文档和 *Microsoft Windows 内部机制* ，并标记和 David 所罗门群岛。

有关其他缓存管理扩展的信息，请参阅 [**！ cchelp**](-cchelp.md) extension。

 

 





