---
title: .settings（指定调试设置）
description: Settings 命令设置、修改、显示、加载和保存调试器中的设置。设置命名空间。
keywords:
- 。设置 (设置调试设置) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .settings (Set Debug Settings)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 906d3c30c1d6cde3e2ea7a012be5d4d7ffe79bd4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799861"
---
# <a name="settings-set-debug-settings"></a>.settings（指定调试设置）


**Settings** 命令设置、修改、显示、加载和保存调试器中的设置。设置命名空间。

```dbgcmd
.settings set  namespace.setting=value
.settings set namespace.setting+=value 
.settings save [file path] 
.settings load file path
.settings list [namespace][-v]
.settings help   
```

## <a name="span-idddk_meta_set_symbol_path_dbgspanspan-idddk_meta_set_symbol_path_dbgspanparameters"></a><span id="ddk_meta_set_symbol_path_dbg"></span><span id="DDK_META_SET_SYMBOL_PATH_DBG"></span>参数


**。设置设置参数**

<span id="_______NAMESPACE.SETTING_VALUE______"></span>**命名空间。设置 = 值**   
设置或修改设置。 指定文件路径时，请使用反斜杠转义，例如 C： \\ \\ 符号 \\ \\ 。

示例：

`.settings set Display.PreferDMLOutput=false`

`.settings set Sources.DisplaySourceLines=true`

`.settings set Symbols.Sympath="C:\\Symbols\\"`

<span id="_______NAMESPACE.SETTING__VALUE______"></span>**命名空间。设置 + = 值**   
指定新值将追加到 (而不是替换以前的值) 。

示例：

`.settings set Extensions.ExtensionSearchPath+=";C:\\MyExtension\\"`

**。设置保存参数**

<span id="_______file_path______"></span><span id="_______FILE_PATH______"></span>**文件路径**   
将调试器. Settings 命名空间中的所有值保存到指定的 XML 文件。

<span id="_______none______"></span><span id="_______NONE______"></span>**无**   
如果未提供文件路径，则会将设置保存到上次加载或保存到的文件。 如果以前的文件不存在，则会在从中加载调试器可执行文件的目录中创建一个名为 config.xml 的文件。

**。正在设置加载参数**

<span id="_______file_path______"></span><span id="_______FILE_PATH______"></span>**文件路径**   
从 XML 设置文件加载所有设置。 加载设置将仅更改该文件中定义的设置。 不会在该文件中显示任何以前加载或更改的设置。 在下一次保存或加载操作之前，此文件将被视为默认的保存路径。

**。正在设置列表参数**

<span id="_______namespace______"></span><span id="_______NAMESPACE______"></span>**命名空间**   
列出给定命名空间中的所有设置及其值。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
– V 标志将导致显示设置说明。

**。设置帮助参数**

<span id="_______None______"></span><span id="_______none______"></span><span id="_______NONE______"></span>**无**   
列出调试器命名空间中的所有设置及其说明。

<span id="_______Namespace______"></span><span id="_______namespace______"></span><span id="_______NAMESPACE______"></span>**命名空间**   
列出给定命名空间中的所有设置及其说明。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

启动时，调试程序将加载调试器可执行文件所在的目录中 config.xml 的所有设置。 在调试会话中，你可以使用以前的设置命令 (例如 sympath 或) 使用 dml 来修改设置。 \_ 你可以使用 ". settings save" 将设置保存到设置配置文件。 可以使用以下命令启用自动保存。

`.settings set AutoSaveSettings=true`

启用自动保存后，调试器中的设置将在退出调试器时自动保存。

<a name="remarks"></a>备注
-------

你可以与其他用户交换 xml 设置文件，以便复制其调试设置。

 

 





