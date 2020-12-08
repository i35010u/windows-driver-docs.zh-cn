---
title: amli 集
description: Amli 设置扩展会设置或显示 AMLI 调试器选项。
keywords:
- amli 设置 Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli set
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36806196bcd7fab2ea0a3d2188737a38fd11265c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800053"
---
# <a name="amli-set"></a>!amli set


**！ Amli set** extension 设置或显示 amli 调试器选项。

```dbgcmd
    !amli set Options
```

## <a name="span-idddk__amli_set_dbgspanspan-idddk__amli_set_dbgspanparameters"></a><span id="ddk__amli_set_dbg"></span><span id="DDK__AMLI_SET_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
指定要设置的一个或多个选项。 用空格分隔多个选项。 可能的值包括：

<span id="spewon"></span><span id="SPEWON"></span>**spewon**  
导致从目标计算机发送完整的调试输出。 对于有效的 AML 调试，应始终保持此选项。 有关详细信息，请参见“备注”部分。

<span id="spewoff"></span><span id="SPEWOFF"></span>**spewoff**  
禁止调试输出。

<span id="verboseon"></span><span id="VERBOSEON"></span>**verboseon**  
启用详细模式。 这将导致 AMLI 调试器在计算 AML 方法时显示其名称。

<span id="verboseoff"></span><span id="VERBOSEOFF"></span>**verboseoff**  
关闭详细模式。

<span id="traceon"></span><span id="TRACEON"></span>**traceon**  
激活 ACPI 跟踪。 与 **verboseon** 选项相比，这会产生更多的输出。 此选项对于跟踪与 SMI-S 相关的硬挂起非常有用。

<span id="traceoff"></span><span id="TRACEOFF"></span>**traceoff**  
停用 ACPI 跟踪。

<span id="nesttraceon"></span><span id="NESTTRACEON"></span>**nesttraceon**  
激活嵌套跟踪。 仅当选择了 **traceon** 选项时，此选项才有效。

<span id="dbgbrkon"></span><span id="DBGBRKON"></span>**dbgbrkon**  
允许中断到 AMLI 调试器。

<span id="dbgbrkoff"></span><span id="DBGBRKOFF"></span>**dbgbrkoff**  
停用 dbgbrkon 选项。

<span id="nesttraceoff"></span><span id="NESTTRACEOFF"></span>**nesttraceoff**  
停用嵌套跟踪。

<span id="lbrkon"></span><span id="LBRKON"></span>**lbrkon**  
完成 DDB 加载后中断 AMLI 调试器。

<span id="lbrkoff"></span><span id="LBRKOFF"></span>**lbrkoff**  
停用 **lbrkon** 选项。

<span id="errbrkon"></span><span id="ERRBRKON"></span>**errbrkon**  
每当解释器在计算 AML 代码时出现问题时，中断到 AMLI 调试器。

<span id="errbrkoff"></span><span id="ERRBRKOFF"></span>**errbrkoff**  
停用 **errbrkon** 选项。

<span id="logon"></span><span id="LOGON"></span>**注册**  
启用事件日志记录。

<span id="logoff"></span><span id="LOGOFF"></span>**注销**  
禁用事件日志记录。

<span id="logmuton"></span><span id="LOGMUTON"></span>**logmuton**  
启用互斥事件日志记录。

<span id="logmutoff"></span><span id="LOGMUTOFF"></span>**logmutoff**  
禁用互斥事件日志记录。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

如果未指定任何选项，将显示所有选项的当前状态。

默认情况下，筛选掉多条消息，可能需要使用 **！ amli set spewon** 启用此输出。 否则，很多 AMLI 调试器消息将丢失。

如果 AML 解释器中断 AMLI 调试器，此输出将自动打开。

有关此输出筛选的详细信息，请参阅 Windows 驱动程序工具包中的 **DbgPrintEx** 和 **KdPrintEx** (WDK) 文档。

 

 





