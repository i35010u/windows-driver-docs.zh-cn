---
title: ExtExtension
description: ExtExtension 类是表示 EngExtCpp 扩展库的 c + + 类的基类。
keywords:
- ExtExtension Windows 调试
topic_type:
- apiref
api_name:
- ExtExtension
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7c7e9b91ebee0da08a3bf1ed37575d04d6bf2e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819193"
---
# <a name="extextension"></a>ExtExtension


**ExtExtension** 类是表示 EngExtCpp 扩展库的 c + + 类的基类。

**ExtExtension** 类包括以下方法，子类可使用这些方法：

[**初始化**](/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))

[**撤消**](/previous-versions/windows/hardware/previsioning-framework/ff558961(v=vs.85))

[**OnSessionActive**](/previous-versions/windows/hardware/previsioning-framework/ff552312(v=vs.85))

[**OnSessionInactive**](/previous-versions/windows/hardware/previsioning-framework/ff552318(v=vs.85))

[**OnSessionAccessible**](/previous-versions/windows/hardware/previsioning-framework/ff552310(v=vs.85))

[**OnSessionInaccessible**](/previous-versions/windows/hardware/previsioning-framework/ff552315(v=vs.85))

**IsUserMode**

**IsKernelMode**

**IsLiveLocalUser**

**IsMachine32**

**IsCurMachine32**

**IsMachine64**

**IsCurMachine64**

**Is32On64**

**CanQueryVirtual**

**HasFullMemBasic**

**IsExtensionRemote**

**AreOutputCallbacksDmlAware**

**RequireUserMode**

**RequireKernelMode**

[**GetNumUnnamedArgs**](/previous-versions/windows/hardware/previsioning-framework/ff548001(v=vs.85))

[**GetUnnamedArgStr**](/previous-versions/windows/hardware/previsioning-framework/ff549464(v=vs.85))

[**GetUnnamedArgU64**](/previous-versions/windows/hardware/previsioning-framework/ff549465(v=vs.85))

[**HasUnnamedArg**](/previous-versions/windows/hardware/previsioning-framework/ff549733(v=vs.85))

[**GetArgStr**](/previous-versions/windows/hardware/previsioning-framework/ff545586(v=vs.85))

[**GetArgU64**](/previous-versions/windows/hardware/previsioning-framework/ff545596(v=vs.85))

[**HasArg**](/previous-versions/windows/hardware/previsioning-framework/ff549721(v=vs.85))

[**HasCharArg**](/previous-versions/windows/hardware/previsioning-framework/ff549727(v=vs.85))

[**SetUnnamedArg**](/previous-versions/windows/hardware/previsioning-framework/ff556876(v=vs.85))

[**SetUnnamedArgStr**](/previous-versions/windows/hardware/previsioning-framework/ff556878(v=vs.85))

[**SetUnnamedArgU64**](/previous-versions/windows/hardware/previsioning-framework/ff556879(v=vs.85))

[**SetArg**](/previous-versions/windows/hardware/previsioning-framework/ff556614(v=vs.85))

[**SetArgStr**](/previous-versions/windows/hardware/previsioning-framework/ff556618(v=vs.85))

[**SetArgU64**](/previous-versions/windows/hardware/previsioning-framework/ff556622(v=vs.85))

[**GetRawArgStr**](/previous-versions/windows/hardware/previsioning-framework/ff548226(v=vs.85))

**GetRawArgCopy**

**弄**

**不再**

**Err**

**谓词**

**Dml**

**DmlWarn**

**DmlErr**

**DmlVerb**

**DmlCmdLink**

**DmlCmdExec**

**RefreshOutputCallbackFlags**

**WrapLine**

**OutWrapStr**

**OutWrapVa**

**OutWrap**

**DemandWrap**

**AllowWrap**

**TestWrap**

**RequestCircleString**

**CopyCircleString**

**PrintCircleStringVa**

**PrintCircleString**

**SetAppendBuffer**

**AppendBufferString**

**AppendStringVa**

**AppendString**

**IsAppendStart**

**SetCallStatus**

**GetCachedSymbolTypeId**

**GetCachedFieldOffset**

**GetCachedFieldOffset**

**AddCachedSymbolInfo**

**GetExpr64**

**GetExprU64**

**GetExprS64**

**ThrowCommandHelp**

**ThrowInterrupt**

**ThrowOutOfMemory**

**ThrowContinueSearch**

**ThrowReloadExtension**

**ThrowInvalidArg**

**ThrowRemote**

**ThrowStatus**

**ThrowLastError**

**ExtExtension** 类还包含子类可以使用的以下字段：

```cpp
class ExtExtension
{
public:
    USHORT  m_ExtMajorVersion;
    USHORT  m_ExtMinorVersion;
    ULONG  m_ExtInitFlags;
    ExtKnownStruct *  m_KnownStructs;
    ExtProvidedValue *  m_ProvidedValues;
    ExtCheckedPointer<IDebugAdvanced>  m_Advanced;
    ExtCheckedPointer<IDebugClient>  m_Client;
    ExtCheckedPointer<IDebugControl>  m_Control;
    ExtCheckedPointer<IDebugDataSpaces>  m_Data;
    ExtCheckedPointer<IDebugRegisters>  m_Registers;
    ExtCheckedPointer<IDebugSymbols>  m_Symbols;
    ExtCheckedPointer<IDebugSystemObjects>  m_System;
    ExtCheckedPointer<IDebugAdvanced2>  m_Advanced2;
    ExtCheckedPointer<IDebugAdvanced3>  m_Advanced3;
    ExtCheckedPointer<IDebugClient2>  m_Client2;
    ExtCheckedPointer<IDebugClient3>  m_Client3;
    ExtCheckedPointer<IDebugClient4>  m_Client4;
    ExtCheckedPointer<IDebugClient5>  m_Client5;
    ExtCheckedPointer<IDebugControl2>  m_Control2;
    ExtCheckedPointer<IDebugControl3>  m_Control3;
    ExtCheckedPointer<IDebugControl4>  m_Control4;
    ExtCheckedPointer<IDebugDataSpaces2>  m_Data2;
    ExtCheckedPointer<IDebugDataSpaces3>  m_Data3;
    ExtCheckedPointer<IDebugDataSpaces4>  m_Data4;
    ExtCheckedPointer<IDebugRegisters2>  m_Registers2;
    ExtCheckedPointer<IDebugSymbols2>  m_Symbols2;
    ExtCheckedPointer<IDebugSymbols3>  m_Symbols3;
    ExtCheckedPointer<IDebugSystemObjects2>  m_System2;
    ExtCheckedPointer<IDebugSystemObjects3>  m_System3;
    ExtCheckedPointer<IDebugSystemObjects4>  m_System4;
    ULONG  m_OutputWidth;
    ULONG  m_ActualMachine;
    ULONG  m_Machine;
    ULONG  m_PageSize;
    ULONG  m_PtrSize;
    ULONG  m_NumProcessors;
    ULONG64  m_OffsetMask;
    ULONG  m_DebuggeeClass;
    ULONG  m_DebuggeeQual;
    ULONG  m_DumpFormatFlags;
    bool  m_IsRemote;
    bool  m_OutCallbacksDmlAware;
    ULONG  m_OutMask;
    ULONG  m_CurChar;
    ULONG  m_LeftIndent;
    bool  m_AllowWrap;
    bool  m_TestWrap;
    ULONG  m_TestWrapChars;
    PSTR  m_AppendBuffer;
    ULONG  m_AppendBufferChars;
    PSTR  m_AppendAt;
};
```

## <a name="span-idmembersspanspan-idmembersspanspan-idmembersspanmembers"></a><span id="Members"></span><span id="members"></span><span id="MEMBERS"></span>组员


<span id="m_ExtMajorVersion"></span><span id="m_extmajorversion"></span><span id="M_EXTMAJORVERSION"></span>**m \_ ExtMajorVersion**  
扩展库的主版本号。 这应由 [**Initialize**](/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85)) 方法设置。 如果未设置，则默认为 **1**。

<span id="m_ExtMinorVersion"></span><span id="m_extminorversion"></span><span id="M_EXTMINORVERSION"></span>**m \_ ExtMinorVersion**  
扩展库的次版本号。 这应由 [**Initialize**](/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85)) 方法设置。 如果未设置，则默认为 **0** (零) 。

<span id="m_ExtInitFlags"></span><span id="m_extinitflags"></span><span id="M_EXTINITFLAGS"></span>**m \_ ExtInitFlags**  
[*DebugExtensionInitialize*](/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_initialize)的 DbgEng 扩展初始化标志。

<span id="m_KnownStructs"></span><span id="m_knownstructs"></span><span id="M_KNOWNSTRUCTS"></span>**m \_ KnownStructs**  
一个 [**ExtKnownStruct**](/windows-hardware/drivers/ddi/engextcpp/ns-engextcpp-extknownstruct) 结构的数组，扩展库可以对输出进行格式设置。 此成员应由 [**Initialize**](/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85)) 方法设置，并且在此方法返回后不应更改。

如果 **m \_ KnownStructs** 不为 **null**，则数组中最后一个 **ExtKnownStruct** 结构的 **TypeName** 成员必须为 **null**。

在格式化目标的输出的结构时，如果结构的类型的名称与此数组中某个 **ExtKnownStruct** 结构的 **TypeName** 成员匹配，则调用 **方法** 成员中指定的回调函数来执行格式设置。

<span id="m_ProvidedValues"></span><span id="m_providedvalues"></span><span id="M_PROVIDEDVALUES"></span>**m \_ ProvidedValues**  
一个 **ExtProvidedValue** 结构的数组，其中列出了扩展库可以为其提供值的伪寄存器。 此成员应由 [**Initialize**](/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85)) 方法设置，并且在此方法返回后不应更改。

如果 **m \_ ProvidedValues** 不为 **null**，则数组中最后一个 **ExtProvidedValue** 结构的 **ValueName** 成员必须为 **null**。

当评估伪寄存器时，如果伪寄存器的名称与此数组中某个 **ExtProvidedValue** 结构的 **ValueName** 成员相匹配，则会调用 **方法** 成员中指定的回调函数来评估伪寄存器。

<span id="m_Advanced"></span><span id="m_advanced"></span><span id="M_ADVANCED"></span>**m \_ 高级**  
扩展库可使用的客户端对象的 [**IDebugAdvanced**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。

<span id="m_Client"></span><span id="m_client"></span><span id="M_CLIENT"></span>**m \_ 客户端**  
扩展库可使用的客户端对象的 [**IDebugClient**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。

<span id="m_Control"></span><span id="m_control"></span><span id="M_CONTROL"></span>**m \_ 控件**  
扩展库可使用的客户端对象的 [**IDebugControl**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。

<span id="m_Data"></span><span id="m_data"></span><span id="M_DATA"></span>**m \_ 数据**  
扩展库可使用的客户端对象的 [**IDebugDataSpaces**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。

<span id="m_Registers"></span><span id="m_registers"></span><span id="M_REGISTERS"></span>**m \_ 寄存器**  
扩展库可使用的客户端对象的 [**IDebugRegisters**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugregisters) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。

<span id="m_Symbols"></span><span id="m_symbols"></span><span id="M_SYMBOLS"></span>**m \_ 符号**  
扩展库可使用的客户端对象的 [**IDebugSymbols**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。

<span id="m_System"></span><span id="m_system"></span><span id="M_SYSTEM"></span>**m \_ 系统**  
扩展库可使用的客户端对象的 [**IDebugSystemObjects**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。

<span id="m_Advanced2"></span><span id="m_advanced2"></span><span id="M_ADVANCED2"></span>**m \_ Advanced2**  
扩展库可使用的客户端对象的 [**IDebugAdvanced2**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Advanced3"></span><span id="m_advanced3"></span><span id="M_ADVANCED3"></span>**m \_ Advanced3**  
扩展库可使用的客户端对象的 [**IDebugAdvanced3**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Client2"></span><span id="m_client2"></span><span id="M_CLIENT2"></span>**m \_ Client2**  
扩展库可使用的客户端对象的 [**IDebugClient2**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Client3"></span><span id="m_client3"></span><span id="M_CLIENT3"></span>**m \_ Client3**  
扩展库可使用的客户端对象的 [**IDebugClient3**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Client4"></span><span id="m_client4"></span><span id="M_CLIENT4"></span>**m \_ Client4**  
扩展库可使用的客户端对象的 [**IDebugClient4**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Client5"></span><span id="m_client5"></span><span id="M_CLIENT5"></span>**m \_ Client5**  
扩展库可使用的客户端对象的 [**IDebugClient5**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Control2"></span><span id="m_control2"></span><span id="M_CONTROL2"></span>**m \_ Control2**  
扩展库可使用的客户端对象的 [**IDebugControl2**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Control3"></span><span id="m_control3"></span><span id="M_CONTROL3"></span>**m \_ Control3**  
扩展库可使用的客户端对象的 [**IDebugControl3**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Control4"></span><span id="m_control4"></span><span id="M_CONTROL4"></span>**m \_ Control4**  
扩展库可使用的客户端对象的 [**IDebugControl4**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Data2"></span><span id="m_data2"></span><span id="M_DATA2"></span>**m \_ Data2**  
扩展库可使用的客户端对象的 [**IDebugDataSpaces2**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Data3"></span><span id="m_data3"></span><span id="M_DATA3"></span>**m \_ Data3**  
扩展库可使用的客户端对象的 [**IDebugDataSpaces3**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Data4"></span><span id="m_data4"></span><span id="M_DATA4"></span>**m \_ Data4**  
扩展库可使用的客户端对象的 [IDebugDataSpaces4](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Registers2"></span><span id="m_registers2"></span><span id="M_REGISTERS2"></span>**m \_ Registers2**  
扩展库可使用的客户端对象的 [**IDebugRegisters2**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugregisters) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Symbols2"></span><span id="m_symbols2"></span><span id="M_SYMBOLS2"></span>**m \_ Symbols2**  
扩展库可使用的客户端对象的 [**IDebugSymbols2**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_Symbols3"></span><span id="m_symbols3"></span><span id="M_SYMBOLS3"></span>**m \_ Symbols3**  
扩展库可使用的客户端对象的 [**IDebugSymbols3**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_System2"></span><span id="m_system2"></span><span id="M_SYSTEM2"></span>**m \_ System2**  
扩展库可使用的客户端对象的 [**IDebugSystemObjects2**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_System3"></span><span id="m_system3"></span><span id="M_SYSTEM3"></span>**m \_ System3**  
扩展库可使用的客户端对象的 [**IDebugSystemObjects3**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_System4"></span><span id="m_system4"></span><span id="M_SYSTEM4"></span>**m \_ System4**  
扩展库可使用的客户端对象的 [**IDebugSystemObjects4**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects) 接口指针。 它在调用外部调用的扩展方法（例如，扩展命令的执行、对 [*ExtKnownStructMethod*](/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85)) 和 **ExtProvideValueMethod** 的调用）期间有效。 此接口在所有版本的调试器引擎中可能不可用。

<span id="m_PtrSize"></span><span id="m_ptrsize"></span><span id="M_PTRSIZE"></span>**m \_ PtrSize**  
当前目标上的指针的大小。 如果目标使用32位指针，则 **m \_ PtrSize** 为4。 如果目标使用64位指针，则 **m \_ PtrSize** 为8。

<span id="m_AppendBuffer"></span><span id="m_appendbuffer"></span><span id="M_APPENDBUFFER"></span>**m \_ AppendBuffer**  
用于将字符串从扩展库返回到引擎的字符缓冲区。 此缓冲区的大小为 **m \_ AppendBufferChars**。 可使用 **AppendBufferString**、 **AppendStringVa** 和 **AppendString** 方法将字符串写入此缓冲区。

<span id="m_AppendBufferChars"></span><span id="m_appendbufferchars"></span><span id="M_APPENDBUFFERCHARS"></span>**m \_ AppendBufferChars**  
缓冲区的大小（以字符为 **\_ AppendBuffer**）。
