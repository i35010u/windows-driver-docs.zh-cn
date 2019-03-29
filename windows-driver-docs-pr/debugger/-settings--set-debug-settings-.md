---
title: .settings（指定调试设置）
description: .Settings 命令设置、 修改、 显示、 加载和保存 Debugger.Settings 命名空间中的设置。
ms.assetid: DAD68FA5-21EF-4A5C-8E5E-0C763CD28C44
keywords:
- .settings （集调试设置） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .settings (Set Debug Settings)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed27d34f56ab44d8b9e2170a02cae120d218eb4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566486"
---
# <a name="settings-set-debug-settings"></a>.settings（指定调试设置）


**.Settings**命令设置、 修改、 显示、 加载和保存 Debugger.Settings 命名空间中的设置。

```dbgcmd
.settings set  namespace.setting=value
.settings set namespace.setting+=value 
.settings save [file path] 
.settings load file path
.settings list [namespace][-v]
.settings help   
```

## <a name="span-idddkmetasetsymbolpathdbgspanspan-idddkmetasetsymbolpathdbgspanparameters"></a><span id="ddk_meta_set_symbol_path_dbg"></span><span id="DDK_META_SET_SYMBOL_PATH_DBG"></span>参数


**.settings 设置参数**

<span id="_______NAMESPACE.SETTING_VALUE______"></span> **namespace.setting=value**   
设置或修改设置。 在指定文件路径使用反斜杠转义，例如 c:\\\\符号\\\\。

示例：

`.settings set Display.PreferDMLOutput=false`

`.settings set Sources.DisplaySourceLines=true`

`.settings set Symbols.Sympath="C:\\Symbols\\"`

<span id="_______NAMESPACE.SETTING__VALUE______"></span> **namespace.setting+=value**   
指定新值将追加到 （而不是替换） 以前的值。

例如：

`.settings set Extensions.ExtensionSearchPath+=";C:\\MyExtension\\"`

**将参数保存.setting**

<span id="_______file_path______"></span><span id="_______FILE_PATH______"></span> **文件路径**   
保存到指定的 XML 文件 Debugger.Settings 命名空间中的所有值。

<span id="_______none______"></span><span id="_______NONE______"></span> **none**   
如果未提供文件路径，设置将保存到上次已加载或保存到的文件。 如果以前的文件不存在，将调试器可执行文件已加载从目录中创建一个名为 config.xml 文件。

**.setting 加载参数**

<span id="_______file_path______"></span><span id="_______FILE_PATH______"></span> **文件路径**   
从 XML 设置文件加载所有设置。 正在加载设置将更改仅在该文件中定义的设置。 将不会修改不会出现在该文件中的任何以前加载的或更改设置。 此文件将被视为作为默认的保存路径，直到下一个保存或加载操作。

**.setting 列表参数**

<span id="_______namespace______"></span><span id="_______NAMESPACE______"></span> **namespace**   
列出给定命名空间和它们的值中的所有设置。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
– V 标记会设置要显示的说明。

**.setting 帮助参数**

<span id="_______None______"></span><span id="_______none______"></span><span id="_______NONE______"></span> **无**   
列出所有调试器命名空间和及其说明中的设置。

<span id="_______Namespace______"></span><span id="_______namespace______"></span><span id="_______NAMESPACE______"></span> **Namespace**   
列出了在给定的命名空间和及其说明的所有设置。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

启动时，调试器将从 config.xml 调试器可执行文件中的目录中加载所有设置。 在调试会话中，您可以修改使用以前的设置命令的设置 (如.sympath 或.prefer\_dml) 或新.settings 命令。 可以使用.settings 保存以将你的设置保存到您的设置配置文件。 可以使用以下命令以启用自动保存。

`.settings set AutoSaveSettings=true`

启用自动保存后，退出调试器时，将自动保存 Debugger.Settings 命名空间中的设置。

<a name="remarks"></a>备注
-------

你可以在交换与其他人要复制其调试设置调试 xml 设置文件。

 

 





