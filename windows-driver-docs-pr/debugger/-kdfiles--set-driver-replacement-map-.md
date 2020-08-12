---
title: .kdfiles（设置驱动程序替换映射）
description: Kdfiles 命令读取文件，并使用其内容作为驱动程序替换图。
ms.assetid: 3b0ac8c1-f0bd-4878-9303-23d6999650ee
keywords:
- 设置驱动程序替换映射 ( kdfiles) 命令
- 驱动程序替换地图，设置驱动程序替换地图 ( kdfiles) 命令
- kdfiles (设置驱动程序替换映射) Windows 调试
ms.date: 08/11/2020
topic_type:
- apiref
api_name:
- .kdfiles (Set Driver Replacement Map)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9c0ce79da0903f46e0323af8b2b125d2ed7fce66
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148432"
---
# <a name="kdfiles-set-driver-replacement-map"></a>.kdfiles（设置驱动程序替换映射）

**Kdfiles**命令读取文件，并使用其内容作为驱动程序替换图。

```dbgcmd
.kdfiles MapFile
.kdfiles -m OldDriver NewDriver
.kdfiles -s SaveFile
.kdfiles -c
.kdfiles
```

## <a name="span-idddk_meta_set_driver_replacement_map_dbgspanspan-idddk_meta_set_driver_replacement_map_dbgspanparameters"></a><span id="ddk_meta_set_driver_replacement_map_dbg"></span><span id="DDK_META_SET_DRIVER_REPLACEMENT_MAP_DBG"></span>参数


<span id="_______MapFile______"></span><span id="_______mapfile______"></span><span id="_______MAPFILE______"></span>*映射*   
指定要读取的驱动程序替换映射文件。

<span id="_______-m______"></span><span id="_______-M______"></span>**-m**   
将驱动程序替换关联添加到当前关联列表。

<span id="_______OldDriver______"></span><span id="_______olddriver______"></span><span id="_______OLDDRIVER______"></span>*OldDriver*   
指定目标计算机上先前驱动程序的路径和文件名。 *OldDriver*的语法与**映射**到驱动程序替换文件中的第一行后的语法相同。 有关此语法的详细信息，请参阅 [映射驱动程序文件](mapping-driver-files.md)。

<span id="_______NewDriver______"></span><span id="_______newdriver______"></span><span id="_______NEWDRIVER______"></span>*NewDriver*   
指定新驱动程序的路径和文件名。 此驱动程序可以位于主计算机上，也可以位于其他某个网络位置。 *NewDriver*的语法与**映射**到驱动程序替换文件中的第二行的语法相同。 有关此语法的详细信息，请参阅 [映射驱动程序文件](mapping-driver-files.md)。

<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
创建一个文件，并将当前的驱动程序替换关联写入该文件。

<span id="_______SaveFile______"></span><span id="_______savefile______"></span><span id="_______SAVEFILE______"></span>*SaveFile*   
指定要创建的文件的名称。

<span id="_______-c______"></span><span id="_______-C______"></span>**-c**   
删除现有的驱动程序替换图。  (此选项不会更改映射文件本身。 相反，此选项将清除调试器的当前映射设置。 ) 

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>基于 x86 的处理器</p></td>
</tr>
</tbody>
</table>

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关驱动程序替换的详细信息以及替换其他内核模式模块的示例、驱动程序替换映射文件的格式说明以及使用此功能的限制，请参阅 [映射驱动程序文件](mapping-driver-files.md)。

<a name="remarks"></a>备注
-------

如果使用不带参数的 **kdfiles** 命令，则调试器将显示当前驱动程序替换映射文件的路径和名称以及替换关联的当前集合。

当你运行此命令时，将读取指定的 *映射*文件。 如果找不到该文件或该文件不包含采用正确格式的文本，则调试器会显示一条消息，指出 "无法加载文件关联"。

如果指定的文件采用正确的驱动程序替换映射文件格式，则调试器会加载文件的内容，并将其用作驱动程序替换映射。 此图将一直保留，直到你退出调试器，或在你发出其他 **的 kdfiles** 命令。

读取该文件之后，驱动程序替换映射不会受对文件 (的后续更改的影响，除非这些更改后跟 **kdfiles** 命令) 。

<a name="user-mode-file-replacement"></a>用户模式文件替换
-------

Windows 版本2004中添加了用户模式文件替换。 此支持允许将以下用户模式文件替换为 kdfiles。

- 用户模式 Dll 还 (包含 NTDLL.DLL 和 KnownDlls) 
- 作为 CreateProcess 的主要进程映像的用户模式 Exe

若要使用用户模式，需要先使用调试程序命令启用内核符号加载， `!gflag +ksl` 或在注册表中配置 ksl 全局标志。 有关 gflag 的详细信息，请参阅 [！ gflag](-gflag.md)。

下面的示例说明了常见的用法。

```dbgcmd
.kdfiles -m system32\userdll C:\myfiles\my_native_userdll.dll
.kdfiles -m system32\userdll \\server\share\my_native_userdll.dll
.kdfiles -m syswow64\ntdll.dll \\server\share\my_x86_wow64_ntdll.dll
.kdfiles -m system32\userbase.dll \\server\share\my_native_userbase.dll
```

用户模式。 kdfiles 将忽略任何与文件匹配的错误，并且不会在发生故障时显示错误消息。

请注意正确限定用户模式. kdfiles 的 kdfiles 路径。 如果只是匹配 ntdll.dll (而不是 system32\ntdll.dll) ，则这是一种不好的做法。 其他不明确的子字符串匹配可能会出现类似的情况。

生成20172后，用户模式. kdfiles 机制将尝试从调试器请求文件，直到一次尝试失败;然后，将不会再次为启动会话重试无法请求的文件名，无需手动干预调试程序即可修改目标系统状态。 在较早的版本中，用户模式 kdfiles 机制将 (成功还是不) 请求每个启动会话的给定文件名。 这些策略降低了与调试程序通信的开销，这些文件不在 kdfiles 列表中，或者无法进行替换，例如由于共享可能已加载了给定文件的进程而导致的冲突。 由于此行为，通常建议将任何文件配置为提前在 kdfiles 列表中拉取，然后再将其引用。

请注意，不能替换已在使用磁盘文件等中的限制。在最初加载多个系统 Dll 后，不能轻松地对其进行热插拔，因此预设了 gflags + ksl 选项，并在启动时使用 kdfiles 来替换任何用户模式的二进制文件。

有关启用启动调试的详细信息，请参阅 [BCDEdit/bootdebug](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--bootdebug)。

建议使用高速/低延迟 KD transport KDNET 来最大程度地降低系统性能影响。

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
<td align="left"><p>在 Windows XP 和更高版本的 Windows 操作系统中受支持。</p></td>
</tr>
</tbody>
</table>

 

 





