---
title: std_map
description: Std_map 扩展显示标准映射树的条目。
ms.assetid: 7a921226-e7b1-4c3f-9732-c53c66710ccb
keywords:
- std_map Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- std_map
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ddfd3297c1539096b9fb6980cb7d48539a6ba0b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338790"
---
# <a name="stdmap"></a>!std\_map


**！ Std\_映射**扩展显示的 std:: map 树条目。

```dbgcmd
!std_map Address [Module!Type [TypeSize]]
!std_map -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的 std:: map 树的地址。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
指定在其中定义数据结构的模块。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *Type*   
指定数据结构的名称。 这必须以表示<em>模块</em>**！ std:: pair&lt;**<em>Type1</em>**，**<em>Type2</em> **&gt;** 窗体。 如果*排字尺寸*参数，此参数必须括在引号中。

<span id="_______TypeSize______"></span><span id="_______typesize______"></span><span id="_______TYPESIZE______"></span> *TypeSize*   
指定要明确符号的数据结构的大小。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简要帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

若要显示其他标准模板库 (STL) 定义的模板，请参阅[ **！ stl**](-stl.md)。

<a name="remarks"></a>备注
-------

其中包括<em>模块</em>**！**<em>类型</em>选项将导致每个条目中要解释为具有给定的类型的表。

使用[ **dt ve (模块 ！ std:: pair&lt;Type1、 Type2&gt;)** ](dt--display-type-.md)以显示可能的大小。

 

 





