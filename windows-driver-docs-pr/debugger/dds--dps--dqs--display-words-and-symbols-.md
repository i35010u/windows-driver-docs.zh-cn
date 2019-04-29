---
title: dds、dps、dqs（显示单词和符号）
description: Dds、 分发点和 dqs 命令显示给定范围中的内存内容。 此内存被假定为一系列符号表中的地址。
ms.assetid: 5a3ed1c4-723a-4902-bfbf-d4a44d2cd0b5
keywords:
- dds，dps，dqs （显示单词和符号） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dds, dps, dqs (Display Words and Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e6754c4089f04672bfae8b65825e4a8923ab5b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373379"
---
# <a name="dds-dps-dqs-display-words-and-symbols"></a>dds、dps、dqs（显示单词和符号）


**Dds**， **dps**，并**dqs**命令显示给定范围中的内存内容。 此内存被假定为一系列符号表中的地址。 还显示相应的符号。

```dbgcmd
dds [Options] [Range] 
dqs [Options] [Range] 
dps [Options] [Range] 
```

## <a name="span-idddkcmddisplaywordsandsymbolsdbgspanspan-idddkcmddisplaywordsandsymbolsdbgspanparameters"></a><span id="ddk_cmd_display_words_and_symbols_dbg"></span><span id="DDK_CMD_DISPLAY_WORDS_AND_SYMBOLS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定一个或多个显示选项。 任何下列选项可以包含，只不过最多只有一个 **/p** \*选项，可以指定：

<span id="_c_Width"></span><span id="_c_width"></span><span id="_C_WIDTH"></span>**/c** *Width*  
指定要在显示中使用列的数。 如果省略，默认列数取决于显示类型。 由于这些命令显示符号的方式，是通常最好使用默认值为只有一个数据列。

<span id="_p"></span><span id="_P"></span>**/p**  
（仅内核模式）使用的显示器的物理内存地址。 指定的范围*范围*来自物理内存而不是虚拟内存。

<span id="_p_c_"></span><span id="_P_C_"></span>**/p\[c\]**  
（仅内核模式）与相同 **/p**，只不过将读取内存缓存。 用方括号括起**c**必须包含。

<span id="_p_uc_"></span><span id="_P_UC_"></span>**/p\[uc\]**  
（仅内核模式）与相同 **/p**，只不过将读取未缓存的内存。 用方括号括起**uc**必须包含。

<span id="_p_wc_"></span><span id="_P_WC_"></span>**/p\[wc\]**  
（仅内核模式）与相同 **/p**，只不过将读写组合内存。 用方括号括起**wc**必须包含。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
指定要显示的内存区域。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。 如果省略*范围*，该命令将显示最后一个命令中显示的结束位置开始的内存。 如果*范围*是省略和没有上一个显示使用命令，显示在当前指令指针开始。 如果给定一个简单的地址，则默认范围长度为 128 个字节。

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

第二个字符**dds**区分大小写。 所有这些命令的第三个字符是区分大小写。

**Dds**命令显示双字 （4 字节） 值，如[ **dd** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令。 **Dqs**命令将显示四字 （8 个字节） 值，如**dq**命令。 **Dps**命令显示指针大小值 （4 字节或 8 个字节，具体取决于目标计算机的体系结构） 等**dp**命令。

所有这些单词被视为在符号表中的地址。 为每个单词显示相应的符号信息。

如果已启用行号信息，源文件名和行号将显示可用时。

 

 





