---
title: 使用 NDIS 驱动程序的函数角色类型来声明函数
description: 使用 NDIS 驱动程序的函数角色类型来声明函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b52df051f65211bd01a70362d779d8526915615a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817833"
---
# <a name="declaring-functions-by-using-function-role-types-for-ndis-drivers"></a>使用 NDIS 驱动程序的函数角色类型来声明函数


若要使 SDV 能够分析 NDIS 驱动程序，必须使用适用于 NDIS 的函数角色类型声明来声明函数。 函数角色类型在 Ndis 中定义。

有关函数角色类型及其相应事件回调函数的列表，请参阅 [静态驱动程序验证器 NDIS 函数声明](static-driver-verifier-ndis-function-declarations.md)。

必须通过指定相应的角色类型声明 NDIS 驱动程序中的每个回调函数。

下面的代码示例演示了 *MiniportPause* 回调函数的函数角色类型声明。 在此示例中，回调函数称为 *myMiniportPause*。 函数角色类型为 "微型端口 \_ 暂停"。

```
MINIPORT_PAUSE myMiniportPause;
```

如果回调函数具有函数原型声明，则必须将函数原型替换为函数角色类型声明。

下面的示例演示了标头文件 MP 中的 NDIS 函数声明，它位于 WDK 的 SDV fail \_ 驱动程序子目录中。 相关函数在 Main. c 中声明。

\\工具 \\ sdv \\ 示例 \\ 失败 \_ 驱动 \\ 程序 \\ NDIS \_ driver1 失败。

```
/--------------------------------------
// Miniport routines in MAIN.C
//--------------------------------------

NDIS_STATUS
DriverEntry(
    IN  PDRIVER_OBJECT      DriverObject,
    IN  PUNICODE_STRING     RegistryPath
    );


MINIPORT_ALLOCATE_SHARED_MEM_COMPLETE MPAllocateComplete;

MINIPORT_HALT MPHalt;
MINIPORT_SET_OPTIONS MPSetOptions;
MINIPORT_INITIALIZE MPInitialize;
MINIPORT_PAUSE MPPause;
MINIPORT_RESTART MPRestart;
MINIPORT_OID_REQUEST MPOidRequest;
MINIPORT_INTERRUPT_DPC MPHandleInterrupt;
MINIPORT_ISR MPIsr;
MINIPORT_RESET MPReset;
MINIPORT_RETURN_NET_BUFFER_LISTS MPReturnNetBufferLists;
MINIPORT_CANCEL_OID_REQUEST MPCancelOidRequest;
MINIPORT_SHUTDOWN MPShutdown;
MINIPORT_SEND_NET_BUFFER_LISTS MPSendNetBufferLists;
MINIPORT_CANCEL_SEND MPCancelSendNetBufferLists;
MINIPORT_DEVICE_PNP_EVENT_NOTIFY MPPnPEventNotify;
MINIPORT_UNLOAD MPUnload;
MINIPORT_CHECK_FOR_HANG MPCheckForHang;
MINIPORT_ENABLE_INTERRUPT MpEnableInterrupt;
MINIPORT_DISABLE_INTERRUPT MpDisableInterrupt;
MINIPORT_SYNCHRONIZE_INTERRUPT MPSynchronizeInterrupt;
MINIPORT_PROCESS_SG_LIST MPProcessSGList;
NDIS_TIMER_FUNCTION MpDemonstrationTimer;
NDIS_IO_WORKITEM MPQueuedWorkItem;
```

### <a name="span-idfunction_parameters_and_function_role_typesspanspan-idfunction_parameters_and_function_role_typesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>函数参数和函数角色类型

根据 C 编程语言的要求，在函数定义中使用的参数类型必须与函数原型的参数类型匹配，在本例中为函数角色类型。 SDV 依赖于用于分析的函数签名，并忽略其签名不匹配的函数。

例如，你应该使用微型端口 [*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr) \_ ISR 函数角色类型声明一个 MiniportInterrupt 函数：

```
MINIPORT_ISR myMPIsr;
```

实现中断例程 *myMPIsr* 时，参数类型必须与微型端口 ISR 使用的参数类型 \_ （即 NDIS \_ 句柄、PBOOLEAN 和 PULONG） (参阅) 语法的 [*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr) 函数。

```
BOOLEAN 
myMPIsr(
    __in  NDIS_HANDLE      MiniportInterruptContext,
    __out PBOOLEAN        QueueMiniportInterruptDpcHandler,
    __out PULONG          TargetProcessors
    ) {
}
```

## <a name="span-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspanspan-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span> 为驱动程序运行代码分析来验证函数声明


为帮助您确定是否已准备好源代码，请 [对驱动程序运行代码分析](code-analysis-for-drivers.md)。 用于驱动程序的代码分析检查函数角色类型声明，并有助于识别可能已丢失的函数声明，或函数定义的参数与函数角色类型中的参数不匹配时发出警告。

 

