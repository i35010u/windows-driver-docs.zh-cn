---
title: ds、dS（显示字符串）
description: Ds 和 dS 命令显示字符串、 ANSI_STRING 或 UNICODE_STRING 结构。
ms.assetid: cb05e89c-6c83-476b-a577-a6aeefd8cdd6
keywords:
- ds，dS （显示字符串） Windows 调试
ms.date: 05/03/2018
topic_type:
- apiref
api_name:
- ds, dS (Display String)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a03159b71e8194b825ffb1df2f40c32ba20d8eaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377762"
---
# <a name="ds-ds-display-string"></a>ds、dS（显示字符串）


**Ds**并**dS**命令将显示一个字符串，ANSI\_字符串或 UNICODE\_字符串*结构*。 

这些命令不会显示 null 分隔的字符串，但而不字符串结构。

如果你有一个 Unicode 字符串的字符的地址然后使用 du 命令。 Da 命令用于显示 ASCII 字符。 有关详细信息，请参阅[d、 da、 db、 dc、 dd、 dD、 df、 dp、 dq、 du，dw （显示内存）](https://docs.microsoft.com/windows-hardware/drivers/debugger/d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor)。

```dbgcmd
d{s|S} [/c Width] [Address]
```

## <a name="span-idddkcmddisplaystringdbgspanspan-idddkcmddisplaystringdbgspanparameters"></a><span id="ddk_cmd_display_string_dbg"></span><span id="DDK_CMD_DISPLAY_STRING_DBG"></span>参数


<span id="_______s______"></span><span id="_______S______"></span> **s**   
指定的字符串或 ANSI\_字符串结构的显示。 (这**s**区分大小写。)

<span id="_______S______"></span><span id="_______s______"></span> **S**   
指定的 UNICODE\_字符串结构的显示。 (这**S**区分大小写。)

<span id="________c_______Width______"></span><span id="________c_______width______"></span><span id="________C_______WIDTH______"></span> **/c** *Width*   
指定要在每一行上显示字符的数。 此数字包括 null 字符，这将不可见。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
内存地址 where UNICODE_STRING 结构存储。 

有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。 如果省略，则假定显示命令中使用的最后一个地址。

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

内存操作的概述和其他与内存相关的命令的说明，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果你想要在局部变量窗口或监视窗口的 WinDbg 中显示的 Unicode 字符串，您必须使用[ **.enable\_（启用 Unicode 显示） 的 unicode** ](-enable-unicode--enable-unicode-display-.md)首先命令。

 

 





