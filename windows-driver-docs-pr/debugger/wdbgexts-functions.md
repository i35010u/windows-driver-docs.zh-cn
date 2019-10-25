---
title: WdbgExts 函数
description: WdbgExts 函数
ms.assetid: 1b070b0c-575d-4104-af66-e0a2c2f2c1b6
keywords:
- WdbgExts 扩展，函数
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b8d9ad666cc637ed3e66290398fe243cf6089c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834186"
---
# <a name="wdbgexts-functions"></a>WdbgExts 函数


## <span id="ddk_wdbgexts_functions_dbwx"></span><span id="DDK_WDBGEXTS_FUNCTIONS_DBWX"></span>


Wdbgexts 头文件包含以下函数的原型。 这些函数对32位和64位扩展使用相同的原型：

[**GetContext**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545736(v=vs.85))

[**SetContext**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556644(v=vs.85))

[**CheckControlC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_check_control_c)

[**GetCurrentProcessAddr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getcurrentprocessaddr)

[**GetCurrentProcessHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects-getcurrentprocesshandle)

[**GetCurrentThreadAddr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getcurrentthreadaddr)

[**GetDebuggerCacheSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getdebuggercachesize)

[**GetDebuggerData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getdebuggerdata)

[**Disasm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_disasm)

[**dprintf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_output_routine)

[**System.componentmodel.design.serialization.codedomserializerbase.getexpression**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_get_expression)

[**GetExpressionEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getexpressionex)

[**GetInputLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getinputline)

[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)

[**GetKdContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getkdcontext)

[**ReadMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff554287(v=vs.85))

[**SearchMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-searchmemory)

[**WriteMemory**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff561420(v=vs.85))

[**ReadMsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readmsr)

[**WriteMsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writemsr)

[**GetPebAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getpebaddress)

[**ReadPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readphysical)

[**ReadPhysicalWithFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readphysicalwithflags)

[**WritePhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writephysical)

[**WritePhysicalWithFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writephysicalwithflags)

[**GetTebAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-gettebaddress)

[**StackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_stacktrace_routine)

[**GetSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_get_symbol)

[**ReloadSymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-reloadsymbols)

[**GetSetSympath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getsetsympath)

[**TranslateVirtualToPhysical**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-translatevirtualtophysical)

Wdbgexts 头文件包含以下函数的原型。 这些函数对于32位和64位扩展具有不同的原型：

[**ReadControlSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readcontrolspace)

[**ReadControlSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readcontrolspace64)

[**ReadTypedControlSpace32**](https://docs.microsoft.com/previous-versions/ff554339(v=vs.85))

[**ReadTypedControlSpace64**](https://docs.microsoft.com/previous-versions/ff554341(v=vs.85))

[**WriteControlSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writecontrolspace)

[**ReadIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospace)

[**ReadIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospace64)

[**ReadIoSpaceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospaceex)

[**ReadIoSpaceEx64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readiospaceex64)

[**WriteIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospace)

[**WriteIoSpace64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospace64)

[**WriteIoSpaceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospaceex)

[**WriteIoSpaceEx64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writeiospaceex64)

[**SetThreadForOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-setthreadforoperation)

[**SetThreadForOperation64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-setthreadforoperation64)

Wdbgexts 头文件包含以下函数的原型。 这些函数只能在64位扩展中使用：

[**GetFieldData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getfielddata)

[**GetFieldOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols-getfieldoffset)

[**GetFieldValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getfieldvalue)

[**GetShortField**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getshortfield)

[**ReadField**](https://docs.microsoft.com/previous-versions/ff553539(v=vs.85))

[**ReadListEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readlistentry)

[**ReadPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readpointer)

[**WritePointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writepointer)

[**IsPtr64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-isptr64)

[**ReadPtr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readptr)

[**GetTypeSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-gettypesize)

[**InitTypeRead**](https://docs.microsoft.com/previous-versions/ff550953(v=vs.85))

[**InitTypeReadPhysical**](https://docs.microsoft.com/previous-versions/ff550957(v=vs.85))

[**ListType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-listtype)

 

 





