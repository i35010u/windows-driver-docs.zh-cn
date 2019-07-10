---
title: d、 da、 db、 dc、 dd、 dD、 df、 dp、 dq、 du，dw （显示内存）
description: D * 命令显示给定范围中的内存内容。
ms.assetid: deb58b77-6648-466d-be00-e2e0a92895b5
keywords:
- d、 da、 db、 dc、 dd、 dD、 df、 dp、 dq、 du，dw （显示内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- d, da, db, dc, dd, dD, df, dp, dq, du, dw (Display Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f716dad8dc05fffcebc36e961ce7dfbeae815ee2
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716847"
---
# <a name="d-da-db-dc-dd-dd-df-dp-dq-du-dw-display-memory"></a>d、 da、 db、 dc、 dd、 dD、 df、 dp、 dq、 du，dw （显示内存）


**D\*** 命令显示给定范围中的内存内容。

```dbgcmd
d{a|b|c|d|D|f|p|q|u|w|W} [Options] [Range] 
dy{b|d} [Options] [Range] 
d [Options] [Range] 
```

## <a name="span-idddkcmddisplaymemorydbgspanspan-idddkcmddisplaymemorydbgspanparameters"></a><span id="ddk_cmd_display_memory_dbg"></span><span id="DDK_CMD_DISPLAY_MEMORY_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定一个或多个显示选项。 任何下列选项可以包含，只不过最多只有一个 **/p** \*选项，可以指定：

<span id="_cWidth"></span><span id="_cwidth"></span><span id="_CWIDTH"></span> **/c**_Width_  
指定要在显示中使用列的数。 如果省略，默认列数取决于显示类型。

<span id="_p"></span><span id="_P"></span> **/p**  
（仅内核模式）使用的显示器的物理内存地址。 指定的范围*范围*来自物理内存而不是虚拟内存。

<span id="_p_c_"></span><span id="_P_C_"></span> **/p\[c\]**  
（仅内核模式）与相同 **/p**，只不过将读取内存缓存。 用方括号括起**c**必须包含。

<span id="_p_uc_"></span><span id="_P_UC_"></span> **/p\[uc\]**  
（仅内核模式）与相同 **/p**，只不过将读取未缓存的内存。 用方括号括起**uc**必须包含。

<span id="_p_wc_"></span><span id="_P_WC_"></span> **/p\[wc\]**  
（仅内核模式）与相同 **/p**，只不过将读写组合内存。 用方括号括起**wc**必须包含。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
指定要显示的内存区域。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。 如果省略*范围*，该命令将显示最后一个命令中显示的结束位置开始的内存。 如果*范围*是省略和没有上一个显示使用命令，显示在当前指令指针开始。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

|||
|--- |--- |
|模式|用户模式下，内核模式|
|目标|实时、 崩溃转储|
|平台|全部|
 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

内存操作的概述和其他与内存相关的命令的说明，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

显示每个行将后跟该内存中的内容和以下位置的行中包括的第一个字节的地址。

如果省略*范围*，该命令将显示最后一个命令中显示的结束位置开始的内存。 这可以通过内存中连续扫描。

此命令采用以下形式存在。 第二个字符**dd**， **dD**， **dw**，以及**dW**命令是区分大小写，如第三个字符的**dyb**并**dyd**命令。

|Command|显示|
|--- |--- |
|d|这与最新的 d 命令相同的格式显示数据。 如果没有以前的 d 命令已发出，d 具有与数据库相同的效果。 请注意，d 重复以 d 开头的最新命令。 这包括 dda、 ddp、 ddu、 dpa、 dpp、 dpu、 dqa、 dqp、 dqu、 dds、 dps、 dqs、 ds、 dS、 dg、 dl、 dt，和 dv，以及在此页上显示命令。 如果给定 d 后的参数不合适，可能会导致错误。|
|da|ASCII 字符。 每行显示最多 48 个字符。 第一个 null 字节或之前已显示范围中的所有字符，将继续显示。 所有非打印字符，如回车符和换行符，显示为句点 （.）。|
|db|字节值和 ASCII 字符。 每个显示行的地址的第一个字节显示在行中后, 跟最多 16 个十六进制字节值。 字节值后面的相应 ASCII 值。 第八个和第九个十六进制值由连字符 （-） 分隔。 所有非打印字符，如回车符和换行符，显示为句点 （.）。 默认计数是 128 个字节。|
|dc|双字值 （4 字节） 和 ASCII 字符。 每个显示行显示的第一个单词的地址行中和最多八个十六进制字值，以及其 ASCII 等效。 默认计数是 32 dword 值 （128 个字节）。| 
|dd|双字值 （4 个字节为单位）。默认计数是 32 dword 值 （128 个字节）。|
|dD|双精度浮点数 （8 字节为单位）。 默认计数是 15 个数字 （120 字节为单位）。|
|df|单精度浮点数 （4 个字节为单位）。 默认计数是 16 位的号码 （64 个字节）。|
|dp|指针大小值。 此命令相当于 dd 或 dq，具体取决于目标计算机的处理器体系结构是 32 位或 64 位分别。 默认计数为 32 的 dword 值或 16 个四字 （128 个字节）。|
|dq|四字值 （8 字节为单位）。 默认计数是 16 个四字 （128 个字节）。|
|du|Unicode 字符。 每行显示最多 48 个字符。 第一个 null 字节或之前已显示范围中的所有字符，将继续显示。 所有非打印字符，如回车符和换行符，显示为句点 （.）。|
|dw|字值 （2 个字节）。 在行中，最多八个十六进制字值，每个显示行显示的第一个单词的地址。 默认计数是 64 单词 （128 个字节）。|
|dW|字值 （2 个字节） 和 ASCII 字符。 在行中，最多八个十六进制字值，每个显示行显示的第一个单词的地址。 默认计数是 64 单词 （128 个字节）。|
|dyb|二进制值和字节值。 默认计数为 32 个字节。|
|dyd|二进制值和双字值 （4 个字节为单位）。 默认计数是 8 Dword （32 字节）。|

 

如果您试图显示无效的地址，其内容如下所示的问号 ( **？** )。

 

 





