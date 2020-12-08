---
title: std_map
description: Std_map 扩展显示 std 地图树的条目。
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
ms.openlocfilehash: f478ec247d13034b22c7bb94be8bde06da05a4be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814057"
---
# <a name="std_map"></a>！ std \_ 地图


**！ Std \_ map** extension 显示 std：： map 树的条目。

```dbgcmd
!std_map Address [Module!Type [TypeSize]]
!std_map -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的 std：： map 树的地址。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
指定在其中定义数据结构的模块。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span>*类型*   
指定数据结构的名称。 这必须以 <em>Module</em>**！ std： &lt; :p air**<em>Type1</em>**，**<em>Type2</em> **&gt;** 格式表示。 如果使用 *排字* 参数，则此参数必须用引号引起来。

<span id="_______TypeSize______"></span><span id="_______typesize______"></span><span id="_______TYPESIZE______"></span>*排字*   
指定数据结构的大小，以使符号具有歧义。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要显示其他标准模板库 (STL) 定义的模板， [**请参阅 stl**](-stl.md)。

<a name="remarks"></a>备注
-------

包括 <em>模块</em>**！**<em>类型</em> 选项使表中的每个条目都被解释为具有给定的类型。

使用 [**dt-ve (Module！ std：:p air &lt; Type1，Type2 &gt;)**](dt--display-type-.md) 来显示可能的大小。

 

 





