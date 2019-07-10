---
title: dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu（显示引用的内存）
description: Dda、 ddp、 ddu、 dpa、 dpp、 dpu、 dqa、 dqp 和 dqu 命令显示在指定位置的指针、 取消引用该指针和显示相关联的内存。
ms.assetid: af3db4e2-e3fc-4c4d-9432-13b87e699716
keywords:
- dda，ddp，ddu，dpa dpp，dpu，dqa，dqp，dqu （显示引用内存） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dda, ddp, ddu, dpa, dpp, dpu, dqa, dqp, dqu (Display Referenced Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 03d4716690edf384f7aecd056d7a62f41ac89c67
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716846"
---
# <a name="dda-ddp-ddu-dpa-dpp-dpu-dqa-dqp-dqu-display-referenced-memory"></a>dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu（显示引用的内存）


**Dda**， **ddp**， **ddu**， **dpa**， **dpp**， **dpu**， **dqa**， **dqp**，并**dqu**命令显示在指定位置的指针、 取消引用该指针，然后在结果中显示的内存各种格式的位置。

```dbgcmd
ddp [Options] [Range] 
dqp [Options] [Range] 
dpp [Options] [Range] 
dda [Options] [Range] 
dqa [Options] [Range] 
dpa [Options] [Range] 
ddu [Options] [Range] 
dqu [Options] [Range] 
dpu [Options] [Range]
```

## <a name="span-idddkcmddisplayreferencedmemorydbgspanspan-idddkcmddisplayreferencedmemorydbgspanparameters"></a><span id="ddk_cmd_display_referenced_memory_dbg"></span><span id="DDK_CMD_DISPLAY_REFERENCED_MEMORY_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定一个或多个显示选项。 任何下列选项可以包含，只不过最多只有一个 **/p** \*选项，可以指定：

<span id="_cWidth"></span><span id="_cwidth"></span><span id="_CWIDTH"></span> **/c**_Width_  
指定要在显示中使用列的数。 如果省略，默认列数取决于显示类型。 由于这些命令显示指针的方式，是通常最好使用默认值为只有一个数据列。

<span id="_p"></span><span id="_P"></span> **/p**  
（仅内核模式）使用的显示器的物理内存地址。 指定的范围*范围*来自物理内存而不是虚拟内存。

<span id="_p_c_"></span><span id="_P_C_"></span> **/p\[c\]**  
（仅内核模式）与相同 **/p**，只不过将读取内存缓存。 用方括号括起**c**必须包含。

<span id="_p_uc_"></span><span id="_P_UC_"></span> **/p\[uc\]**  
（仅内核模式）与相同 **/p**，只不过将读取未缓存的内存。 用方括号括起**uc**必须包含。

<span id="_p_wc_"></span><span id="_P_WC_"></span> **/p\[wc\]**  
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

此命令的第二个和第三个字符是区分大小写。

此命令的第二个字符确定指针使用大小：

|Command|显示|
|--- |--- |
|dd|所使用的 32 位指针|
|dq|所使用的 64 位指针|
|dp*|使用标准指针大小：32 位或 64 位，具体取决于目标的处理器体系结构|

 

此命令的第三个字符确定取消引用的内存的显示方式：

|Command|显示|
|--- |--- |
|dp|显示格式为 DWORD 或 QWORD，具体取决于目标的处理器体系结构的指针大小指针所引用的内存的内容。 如果此值与匹配任何已知的符号，也将显示此符号。|
|da|显示格式为 ASCII 字符指针所引用的内存的内容。|
|d*u|显示 Unicode 字符格式指针所引用的内存内容。|

 

如果已启用行号信息，源文件名和行号将显示可用时。

 

 





