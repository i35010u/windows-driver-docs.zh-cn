---
title: dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu（显示引用的内存）
description: Dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp 和 dqu 命令在指定位置显示指针，取消引用指针，并显示关联的内存。
keywords:
- dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu (显示引用的内存) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dda, ddp, ddu, dpa, dpp, dpu, dqa, dqp, dqu (Display Referenced Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 001b723f1793d44c87ed32644f6578175b2714d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823451"
---
# <a name="dda-ddp-ddu-dpa-dpp-dpu-dqa-dqp-dqu-display-referenced-memory"></a>dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu（显示引用的内存）


**Dda**、 **ddp**、 **ddu**、 **dpa**、 **dpp**、 **dpu**、 **dqa**、 **dqp** 和 **dqu** 命令将在指定位置显示指针，取消引用该指针，然后以各种格式显示位于结果位置的内存。

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

## <a name="span-idddk_cmd_display_referenced_memory_dbgspanspan-idddk_cmd_display_referenced_memory_dbgspanparameters"></a><span id="ddk_cmd_display_referenced_memory_dbg"></span><span id="DDK_CMD_DISPLAY_REFERENCED_MEMORY_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
指定一个或多个显示选项。 可以包含以下任何选项，但不能指定多个 **/p** \* 选项：

<span id="_cWidth"></span><span id="_cwidth"></span><span id="_CWIDTH"></span>**/c**_Width_  
指定要在显示中使用的列数。 如果省略此值，则默认的列数取决于显示类型。 由于这些命令显示指针的方式，通常最好只使用一个数据列的默认值。

<span id="_p"></span><span id="_P"></span>**/p**  
仅 (内核模式) 使用物理内存地址进行显示。 *范围* 指定的范围将从物理内存而不是虚拟内存中获取。

<span id="_p_c_"></span><span id="_P_C_"></span>**/p \[ c\]**  
 (内核模式仅) 与 **/P** 相同，不同之处在于缓存的内存将被读取。 必须包括 **c** 的方括号。

<span id="_p_uc_"></span><span id="_P_UC_"></span>**/p \[ uc\]**  
 (内核模式仅) 与 **/P** 相同，不同之处在于将读取未缓存的内存。 必须包括 **uc** 周围的方括号。

<span id="_p_wc_"></span><span id="_P_WC_"></span>**/p \[ wc.exe\]**  
 (内核模式仅) 与 **/P** 相同，不同之处在于将读取写入合并内存。 必须包含 **wc.exe** 两侧的方括号。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定要显示的内存区域。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。 如果省略 *Range*，则该命令将显示从上一个显示命令的结束位置开始的内存。 如果省略 *Range* 并且未使用上一个显示命令，则显示从当前指令指针开始。 如果提供了简单地址，则默认范围长度为128字节。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

**模式**：用户模式，内核模式

**目标**：实时、崩溃转储

**平台**：所有

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内存操作的概述以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

此命令的第二个和第三个字符区分大小写。

此命令的第二个字符确定使用的指针大小：

|命令|显示|
|--- |--- |
|dd|使用的32位指针|
|dq|使用的64位指针|
|dp|使用的标准指针大小：32位或64位，具体取决于目标处理器的体系结构|

 

此命令的第三个字符确定如何显示取消引用的内存：

|命令|显示|
|--- |--- |
|dp|显示指针所引用的内存内容（采用 DWORD 或 QWORD 格式），这取决于目标处理器体系结构的指针大小。 如果此值与任何已知符号匹配，也会显示此符号。|
|da|显示指针在 ASCII 字符格式中引用的内存内容。|
|d * u|以 Unicode 字符格式显示指针所引用的内存的内容。|

 

如果已启用行号信息，将显示源文件名和行号（如果可用）。

 

 





