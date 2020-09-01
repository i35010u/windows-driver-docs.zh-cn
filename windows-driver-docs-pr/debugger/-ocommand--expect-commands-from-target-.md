---
title: .ocommand（需要目标提供命令）
description: Ocommand 命令使目标应用程序能够将命令发送到调试器。
ms.assetid: a4363395-111f-48eb-b1da-c17c0ad9f067
keywords:
- 需要来自目标 ( 的命令。 ocommand) 命令
- ocommand (需要来自目标) Windows 调试的命令
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ocommand (Expect Commands from Target)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 180fff3165a51e6f3121c6e5133336bbf5b66fa6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214862"
---
# <a name="ocommand-expect-commands-from-target"></a>.ocommand（需要目标提供命令）


**Ocommand**命令使目标应用程序能够将命令发送到调试器。

```dbgcmd
.ocommand  String 
.ocommand -d 
.ocommand 
```

## <a name="span-idddk_meta_expect_commands_from_target_dbgspanspan-idddk_meta_expect_commands_from_target_dbgspanparameters"></a><span id="ddk_meta_expect_commands_from_target_dbg"></span><span id="DDK_META_EXPECT_COMMANDS_FROM_TARGET_DBG"></span>参数


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span>*字符串*   
指定命令前缀字符串。 *字符串*可以包括空格，但不能使用 C 样式控制字符，例如 "和** \\ n** ** \\ "** 。 还可以将 *字符串* 用引号引起来。 但是，如果 *字符串* 包含分号、前导空格或尾随空格，则必须用引号将 *字符串* 引起来。

<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
删除命令前缀字符串。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关与调试程序通信的 [**OutputDebugString**](/windows/desktop/api/debugapi/nf-debugapi-outputdebugstringw) 和其他用户模式功能的详细信息，请参阅 Microsoft Windows SDK 文档。

<a name="remarks"></a>备注
-------

如果使用不带参数的 **ocommand** 命令，则调试器会显示当前的命令前缀字符串。 若要清除现有字符串，请使用 **ocommand-d**。

设置命令前缀字符串后，将扫描任何目标输出 (如 [**OutputDebugString**](/windows/desktop/api/debugapi/nf-debugapi-outputdebugstringw) 命令) 的内容。 如果此输出以命令前缀字符串开头，则前缀字符串后跟的输出文本将被视为调试器命令字符串并运行。 在执行此文本时，不会显示命令字符串。

如果需要其他消息，目标可以在输出字符串中包含一个 [**回显 (Echo 注释) **](-echo--echo-comment-.md) 命令。 以典型方式显示不以前缀字符串开头的目标输出。

在命令字符串中执行命令后，目标仍会被分解到调试器中，除非最后一个命令为 [**g (转) **](g--go-.md)。

命令前缀字符串与目标输出之间的比较不区分大小写。  (但是，在后续使用的情况下， **将显示你** 在) 保留的情况下输入的字符串。

对于本示例，假定您在调试器中输入以下命令。

```dbgcmd
0:000> .ocommand magiccommand
```

然后，目标应用程序会执行以下行。

```dbgcmd
OutputDebugString("MagicCommand kb;g");
```

调试器会立即识别命令字符串前缀并执行 **kb; g** 。

但是，以下行不会导致执行任何命令。

```dbgcmd
OutputDebugString("Command on next line.\nmagiccommand kb;g");
```

没有从前面的示例中执行命令，因为命令字符串前缀不在输出的开头，即使它确实开始换行。

**注意**   应选择一个命令字符串前缀，该前缀不可能出现在除您自己的命令之外的任何目标输出中。

 

 

