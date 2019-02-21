---
title: .kdfiles (组驱动程序替换 Map)
description: .Kdfiles 命令读取文件，并使用其内容为驱动程序替换映射。
ms.assetid: 3b0ac8c1-f0bd-4878-9303-23d6999650ee
keywords:
- 设置驱动程序替换映射 (.kdfiles) 命令
- 驱动程序替换映射中，设置驱动程序替换映射 (.kdfiles) 命令
- .kdfiles (组驱动程序替换 Map) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .kdfiles (Set Driver Replacement Map)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 95e85cd4e0d5bc300ec195d55d0e25d33891891c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546023"
---
# <a name="kdfiles-set-driver-replacement-map"></a>.kdfiles (组驱动程序替换 Map)


**.Kdfiles**命令读取文件，并使用其内容为驱动程序替换映射。

```dbgcmd
.kdfiles MapFile 
.kdfiles -m OldDriver NewDriver
.kdfiles -s SaveFile 
.kdfiles -c 
.kdfiles 
```

## <a name="span-idddkmetasetdriverreplacementmapdbgspanspan-idddkmetasetdriverreplacementmapdbgspanparameters"></a><span id="ddk_meta_set_driver_replacement_map_dbg"></span><span id="DDK_META_SET_DRIVER_REPLACEMENT_MAP_DBG"></span>参数


<span id="_______MapFile______"></span><span id="_______mapfile______"></span><span id="_______MAPFILE______"></span> *MapFile*   
指定要读取的驱动程序替换映射文件。

<span id="_______-m______"></span><span id="_______-M______"></span> **-m**   
将驱动程序替换关联添加到当前的关联列表。

<span id="_______OldDriver______"></span><span id="_______olddriver______"></span><span id="_______OLDDRIVER______"></span> *OldDriver*   
指定目标计算机上以前的驱动程序的路径和文件名称。 语法*OldDriver*后面的第一个行相同**映射**驱动程序替换文件中。 有关此语法的详细信息，请参阅[映射驱动程序文件](mapping-driver-files.md)。

<span id="_______NewDriver______"></span><span id="_______newdriver______"></span><span id="_______NEWDRIVER______"></span> *NewDriver*   
指定新的驱动程序路径和文件名。 此驱动程序可以在主计算机上或在其他某个网络位置。 语法*NewDriver*后面的第二个行相同**映射**驱动程序替换文件中。 有关此语法的详细信息，请参阅[映射驱动程序文件](mapping-driver-files.md)。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
创建一个文件并写入该文件当前驱动程序替换的关联。

<span id="_______SaveFile______"></span><span id="_______savefile______"></span><span id="_______SAVEFILE______"></span> *SaveFile*   
指定要创建的文件的名称。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
删除现有的驱动程序替换映射。 （此选项不会更改映射文件本身。 相反，此选项将清除调试器的当前映射设置。）

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

可以使用 **.kdfiles**命令，在 Microsoft Windows XP 和更高版本的 Windows。 如果在早期版本的 Windows 中使用此命令，该命令不起作用并不会生成错误。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>基于 x86 和基于 Itanium 的处理器</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和驱动程序替换和替换为其他内核模式模块的示例，请参阅驱动程序替换映射文件的格式和使用此功能的限制的说明[映射驱动程序文件](mapping-driver-files.md).

<a name="remarks"></a>备注
-------

如果您使用 **.kdfiles**命令不带参数，调试器将显示的路径和当前驱动程序替换映射文件的名称和当前的替换关联集。

当运行此命令中，指定*映射文件*读取文件。 如果找不到该文件，或者它不包含采用正确格式的文本，调试器将显示一条消息，指出"无法加载文件关联"。

如果指定的文件是正确的驱动程序替换映射文件格式，调试器加载文件的内容，并将其用作驱动程序替换映射。 此映射保留，直到退出调试器，或直到您发出另一个 **.kdfiles**命令。

读取该文件后，驱动程序替换映射不受对该文件的后续更改 (除非这些更改后跟另 **.kdfiles**命令)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>支持 Windows XP 和更高版本的 Windows 操作系统中。</p></td>
</tr>
</tbody>
</table>

 

 





