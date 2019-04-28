---
title: amli 集
description: Amli 集扩展设置，或显示 AMLI 调试器选项。
ms.assetid: 521fa305-8073-4d94-bc28-fdb35cbc2acd
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
ms.openlocfilehash: e131516c5bf95e19f4277a44ce9a3e59bf175b59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334758"
---
# <a name="amli-set"></a>!amli set


**！ Amli 集**扩展插件设置，或显示 AMLI 调试器选项。

```dbgcmd
    !amli set Options
```

## <a name="span-idddkamlisetdbgspanspan-idddkamlisetdbgspanparameters"></a><span id="ddk__amli_set_dbg"></span><span id="DDK__AMLI_SET_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定一个或多个要设置的选项。 用空格分隔多个选项。 可能值的包括：

<span id="spewon"></span><span id="SPEWON"></span>**spewon**  
会导致输出为从目标计算机发送完整的调试。 此选项应保留在所有时间的有效 AML 调试。 请参阅备注部分了解详细信息。

<span id="spewoff"></span><span id="SPEWOFF"></span>**spewoff**  
禁止显示调试输出。

<span id="verboseon"></span><span id="VERBOSEON"></span>**verboseon**  
开启详细模式。 这将导致 AMLI 调试器来计算它们按显示的 AML 方法的名称。

<span id="verboseoff"></span><span id="VERBOSEOFF"></span>**verboseoff**  
关闭详细模式。

<span id="traceon"></span><span id="TRACEON"></span>**traceon**  
激活 ACPI 跟踪。 这将产生更多输出比**verboseon**选项。 此选项是用于跟踪 SMI 相关硬挂起非常有用。

<span id="traceoff"></span><span id="TRACEOFF"></span>**traceoff**  
ACPI 跟踪将停用。

<span id="nesttraceon"></span><span id="NESTTRACEON"></span>**nesttraceon**  
激活嵌套跟踪。 如果此选项是唯一的有效**traceon**还选择选项。

<span id="dbgbrkon"></span><span id="DBGBRKON"></span>**dbgbrkon**  
启用中断到 AMLI 调试器。

<span id="dbgbrkoff"></span><span id="DBGBRKOFF"></span>**dbgbrkoff**  
停用 dbgbrkon 选项。

<span id="nesttraceoff"></span><span id="NESTTRACEOFF"></span>**nesttraceoff**  
嵌套跟踪将停用。

<span id="lbrkon"></span><span id="LBRKON"></span>**lbrkon**  
DDB 加载完毕后，进入 AMLI 调试器。

<span id="lbrkoff"></span><span id="LBRKOFF"></span>**lbrkoff**  
停用**lbrkon**选项。

<span id="errbrkon"></span><span id="ERRBRKON"></span>**errbrkon**  
每当解释器必须评估 AML 代码问题，请进入 AMLI 调试器。

<span id="errbrkoff"></span><span id="ERRBRKOFF"></span>**errbrkoff**  
停用**errbrkon**选项。

<span id="logon"></span><span id="LOGON"></span>**logon**  
启用事件日志记录功能。

<span id="logoff"></span><span id="LOGOFF"></span>**logoff**  
禁用事件日志记录。

<span id="logmuton"></span><span id="LOGMUTON"></span>**logmuton**  
启用互斥体事件日志记录。

<span id="logmutoff"></span><span id="LOGMUTOFF"></span>**logmutoff**  
禁用互斥体事件日志记录。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

如果未不指定任何选项，显示所有选项的当前状态。

默认情况下，多个消息筛选掉，可能需要将此输出上使用 **！ amli 设置 spewon**。 否则，许多 AMLI 调试器消息将丢失。

如果 AMLI 调试器中中断 AML 解释器，此输出将自动打开。

此输出筛选的详细信息，请参阅**DbgPrintEx**并**KdPrintEx** Windows Driver Kit (WDK) 文档中。

 

 





