---
title: 'd，da，db，dc，dd，dD，df，dp，dq，du，dw (显示内存) '
description: D * 命令显示给定范围内内存的内容。
keywords:
- d，da，db，dc，dd，dD，df，dp，dq，du，dw (显示内存) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- d, da, db, dc, dd, dD, df, dp, dq, du, dw (Display Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27a838ede85f72334b05b0aa048f74b1c967ce43
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839801"
---
# <a name="d-da-db-dc-dd-dd-df-dp-dq-du-dw-display-memory"></a>d，da，db，dc，dd，dD，df，dp，dq，du，dw (显示内存) 


**D \** _ 命令显示给定范围内内存的内容。

```dbgcmd
d{a|b|c|d|D|f|p|q|u|w|W} [Options] [Range] 
dy{b|d} [Options] [Range] 
d [Options] [Range] 
```

## <a name="span-idddk_cmd_display_memory_dbgspanspan-idddk_cmd_display_memory_dbgspanparameters"></a><span id="ddk_cmd_display_memory_dbg"></span><span id="DDK_CMD_DISPLAY_MEMORY_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> _Options *   
指定一个或多个显示选项。 可以包含以下任何选项，但不能指定多个 **/p** \* 选项：

<span id="_cWidth"></span><span id="_cwidth"></span><span id="_CWIDTH"></span>**/c**_Width_  
指定要在显示中使用的列数。 如果省略此值，则默认的列数取决于显示类型。

<span id="_p"></span><span id="_P"></span>**/p**  
仅 (内核模式) 使用物理内存地址进行显示。 *范围* 指定的范围将从物理内存而不是虚拟内存中获取。

<span id="_p_c_"></span><span id="_P_C_"></span>**/p \[ c\]**  
 (内核模式仅) 与 **/P** 相同，不同之处在于缓存的内存将被读取。 必须包括 **c** 的方括号。

<span id="_p_uc_"></span><span id="_P_UC_"></span>**/p \[ uc\]**  
 (内核模式仅) 与 **/P** 相同，不同之处在于将读取未缓存的内存。 必须包括 **uc** 周围的方括号。

<span id="_p_wc_"></span><span id="_P_WC_"></span>**/p \[ wc.exe\]**  
 (内核模式仅) 与 **/P** 相同，不同之处在于将读取写入合并内存。 必须包含 **wc.exe** 两侧的方括号。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定要显示的内存区域。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。 如果省略 *Range*，则该命令将显示从上一个显示命令的结束位置开始的内存。 如果省略 *Range* 并且未使用上一个显示命令，则显示从当前指令指针开始。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

**模式**：用户模式，内核模式

**目标**：实时、崩溃转储

**平台**：所有

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内存操作的概述以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

显示的每一行都将包含行中第一个字节的地址，后跟该位置和以下位置的内存内容。

如果省略 *Range*，则该命令将显示从上一个显示命令的结束位置开始的内存。 这使您可以持续扫描内存。

此命令采用以下形式存在。 **Dd**、 **dd**、 **dw** 和 **dw** 命令的第二个字符区分大小写，这是 **dyb** 和 **dyd** 命令的第三个字符。

|命令|显示|
|--- |--- |
|d|这会将数据显示为与最近 d 命令相同的格式。 如果以前的 d 命令未发出，则 d 与 db 具有相同的效果。 请注意，d 重复了以 d 开头的最新命令。 这包括： dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu、dds、dps、dqs、ds、dS、dg、dl、dt 和 dv，以及此页上的显示命令。 如果 d 之后给出的参数不合适，则可能会导致错误。|
|da|ASCII 字符。 每一行最多可显示48个字符。 显示将继续直到第一个 null 字节或范围内的所有字符都显示出来。 所有非打印字符（如回车符和换行符）都作为句点 ( 显示。 ) 。|
|db|字节值和 ASCII 字符。 每个显示行显示行中第一个字节的地址，后跟多达16个十六进制字节值。 字节值后跟对应的 ASCII 值。 第八个和第九个十六进制值由连字符分隔 ( ) 。 所有非打印字符（如回车符和换行符）都作为句点 ( 显示。 ) 。 默认计数为128字节。|
|dc|双字值 (4 个字节) 和 ASCII 字符。 每个显示行显示行中第一个单词的地址和最多八个十六进制字值及其 ASCII 等效值。 默认计数为 32 Dword (128 字节) 。| 
|dd|双字值 (4 个字节) 。默认计数为 32 Dword (128 字节) 。|
|dD|双精度浮点数字 (8 字节) 。 默认计数为15个数字 (120 字节) 。|
|df|单精度浮点数字 (4 个字节) 。 默认计数为16个数字 (64 字节) 。|
|dp|指针大小的值。 此命令等效于 dd 或 dq，具体取决于目标计算机的处理器体系结构是否分别为32或64。 默认计数为 32 Dword 或16个四字 (128 字节) 。|
|dq|四字值 (8 字节) 。 默认计数为16个四字， (128 字节) 。|
|du|Unicode 字符。 每一行最多可显示48个字符。 显示将继续直到第一个 null 字节或范围内的所有字符都显示出来。 所有非打印字符（如回车符和换行符）都作为句点 ( 显示。 ) 。|
|dw|字值 (2 个字节) 。 每个显示行显示行中第一个单词的地址和最多八个十六进制单词值。 默认计数为64字 (128 字节) 。|
|dW|字值 (2 个字节) 和 ASCII 字符。 每个显示行显示行中第一个单词的地址和最多八个十六进制单词值。 默认计数为64字 (128 字节) 。|
|dyb|二进制值和字节值。 默认计数为32字节。|
|dyd|二进制值和双字值 (4 个字节) 。 默认计数为8个 Dword (32 字节) 。|

 

如果尝试显示无效地址，则其内容将显示为问号 (**？**) 。

 

 





