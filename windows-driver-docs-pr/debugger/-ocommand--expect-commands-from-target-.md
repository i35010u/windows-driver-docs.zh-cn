---
title: .ocommand（需要目标提供命令）
description: .Ocommand 命令启用目标应用程序将命令发送到调试器。
ms.assetid: a4363395-111f-48eb-b1da-c17c0ad9f067
keywords:
- 预期目标 (.ocommand) 命令的命令
- .ocommand （预期目标的命令） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ocommand (Expect Commands from Target)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0fa9315c0da45e0fd15e150745fb3e0bb01c7ca5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362447"
---
# <a name="ocommand-expect-commands-from-target"></a>.ocommand（需要目标提供命令）


**.Ocommand**命令使目标应用程序将命令发送到调试器。

```dbgcmd
.ocommand  String 
.ocommand -d 
.ocommand 
```

## <a name="span-idddkmetaexpectcommandsfromtargetdbgspanspan-idddkmetaexpectcommandsfromtargetdbgspanparameters"></a><span id="ddk_meta_expect_commands_from_target_dbg"></span><span id="DDK_META_EXPECT_COMMANDS_FROM_TARGET_DBG"></span>参数


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *字符串*   
指定的命令前缀字符串。 *字符串*可以包含空格，但不能使用 C 样式控制字符，例如 **\\"** 并 **\\n**。 此外可以包含*字符串*引号引起来。 但是，如果*字符串*包括一个分号，前导空格或尾随空格，则必须将括*字符串*引号引起来。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
删除命令的前缀字符串。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息[ **OutputDebugString** ](https://docs.microsoft.com/windows/desktop/api/debugapi/nf-debugapi-outputdebugstringw)和通信使用调试器，其他用户模式下函数，请参阅 Microsoft Windows SDK 文档。

<a name="remarks"></a>备注
-------

如果您使用 **.ocommand**命令不带参数，则调试器会显示当前的命令前缀字符串。 若要清除现有的字符串，请使用 **.ocommand-d**。

设置命令的前缀字符串后，任何目标输出 (如的内容[ **OutputDebugString** ](https://docs.microsoft.com/windows/desktop/api/debugapi/nf-debugapi-outputdebugstringw)命令) 进行扫描。 如果此输出开头的命令前缀字符串，前缀字符串之后的输出的文本被视为调试器命令字符串，并运行。 执行此文本时，不显示命令字符串。

目标可以包括[ **.echo （Echo 注释）** ](-echo--echo-comment-.md)命令输出字符串中，如果所需的其他消息。 不以开头的前缀字符串的目标输出所示的典型方式。

后该命令中的命令字符串已执行，除非最后一个命令是中断到调试器，该目标将保持[ **g （转向）** ](g--go-.md)。

命令的前缀字符串与目标输出之间的比较不区分大小写。 (但是，后续使用的 **.ocommand**显示您输入与保留的事例的字符串)。

此示例中，假设你在调试器中输入以下命令。

```dbgcmd
0:000> .ocommand magiccommand
```

然后，目标应用程序执行的以下行。

```dbgcmd
OutputDebugString("MagicCommand kb;g");
```

调试器可以识别的命令字符串前缀，并执行**kb; g**立即。

但是，以下行不会导致任何要执行的命令。

```dbgcmd
OutputDebugString("Command on next line.\nmagiccommand kb;g");
```

没有执行的命令从前面的示例中的命令字符串前缀开头的输出中，不是因为即使它才开始新行。

**请注意**  应选择一个命令字符串前缀，不会有可能出现在任何目标输出自己的命令除外。

 

 

 





