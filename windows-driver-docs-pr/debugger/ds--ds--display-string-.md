---
title: ds、dS（显示字符串）
description: Ds 和 dS 命令显示 STRING、ANSI_STRING 或 UNICODE_STRING 结构。
ms.assetid: cb05e89c-6c83-476b-a577-a6aeefd8cdd6
keywords:
- ds、dS (显示字符串) Windows 调试
ms.date: 05/03/2018
topic_type:
- apiref
api_name:
- ds, dS (Display String)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f9ebe09fb97b8fb7b81740d8d45b91052a5bfaec
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209375"
---
# <a name="ds-ds-display-string"></a>ds、dS（显示字符串）


**Ds**和**DS**命令显示字符串、ANSI \_ 字符串或 UNICODE \_ 字符串*结构*。 

这些命令不会显示以 null 分隔的字符串，而是显示字符串结构。

如果你具有 Unicode 字符串的字符的地址，则改为使用 du 命令。 使用 da 命令显示 ASCII 字符。 有关详细信息，请参阅 [d，da，db，dc，dd，dd，df，dp，dq，du，dw (显示内存) ](./d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)。

```dbgcmd
d{s|S} [/c Width] [Address]
```

## <a name="span-idddk_cmd_display_string_dbgspanspan-idddk_cmd_display_string_dbgspanparameters"></a><span id="ddk_cmd_display_string_dbg"></span><span id="DDK_CMD_DISPLAY_STRING_DBG"></span>参数


<span id="_______s______"></span><span id="_______S______"></span>**s**   
指定要显示字符串或 ANSI \_ 字符串结构。  (此 **区分** 大小写。 ) 

<span id="_______S______"></span><span id="_______s______"></span>**S**   
指定将显示 UNICODE \_ 字符串结构。  (此 **区分** 大小写。 ) 

<span id="________c_______Width______"></span><span id="________c_______width______"></span><span id="________C_______WIDTH______"></span>**/c** *Width*   
指定要在每一行上显示的字符数。 此数字包含空字符，这将不可见。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
存储 UNICODE_STRING 结构的的内存地址。 

有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。 如果省略，则假定显示命令中使用的最后一个地址。

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

有关内存操作的概述以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果要在 "局部变量" 窗口或 "WinDbg 监视窗口中显示 Unicode 字符串，则需要使用" [**启用 \_ Unicode (启用 unicode 显示) **](-enable-unicode--enable-unicode-display-.md) 命令。

 

