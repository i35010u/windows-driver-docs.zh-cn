---
title: 使用 NDIS 驱动程序的函数角色类型来声明函数
description: 使用 NDIS 驱动程序的函数角色类型来声明函数
ms.assetid: 232c4272-0bf0-4a4e-9560-3bceeca8a3e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a813e3e039f01d709f52781ed2f88874bb0625d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371560"
---
# <a name="declaring-functions-by-using-function-role-types-for-ndis-drivers"></a>使用 NDIS 驱动程序的函数角色类型来声明函数


若要启用 SDV 要分析的 NDIS 驱动程序，必须使用 NDIS 函数角色类型声明中声明函数。 Ndis.h 中定义的函数角色类型。

有关函数的角色类型和其相应的事件回调函数的列表，请参阅[静态验证工具 NDIS 驱动程序函数声明](static-driver-verifier-ndis-function-declarations.md)。

必须通过指定相应的角色类型声明的 NDIS 驱动程序中每个回调函数。

下面的代码示例演示的函数角色类型声明*MiniportPause*回调函数。 在此示例中，调用该回调函数*myMiniportPause*。 函数角色类型是微型端口\_暂停。

```
MINIPORT_PAUSE myMiniportPause;
```

如果回调函数有函数原型声明，必须将函数原型替换函数角色类型声明。

下面的示例演示从标头文件 MP.h，位于 SDV NDIS 函数声明失败\_WDK 的驱动程序子目录。 相关的函数 Main.c 中声明。

\\工具\\sdv\\示例\\失败\_驱动程序\\NDIS\\失败\_driver1。

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

### <a name="span-idfunctionparametersandfunctionroletypesspanspan-idfunctionparametersandfunctionroletypesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>函数参数和函数的角色类型

根据需要在 C 编程语言中，在函数定义中使用的参数类型必须匹配的函数原型中，参数类型或函数角色在此示例中，键入。 SDV 取决于分析的函数签名，并忽略的函数的签名不匹配。

例如，应声明[ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)函数使用微型端口\_ISR 函数角色类型：

```
MINIPORT_ISR myMPIsr;
```

实现中断例程时*myMPIsr*，参数类型必须匹配所使用的微型端口\_ISR，即 NDIS\_句柄、 PBOOLEAN 和 PULONG (请参阅[ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)语法的函数)。

```
BOOLEAN 
myMPIsr(
    __in  NDIS_HANDLE      MiniportInterruptContext,
    __out PBOOLEAN        QueueMiniportInterruptDpcHandler,
    __out PULONG          TargetProcessors
    ) {
}
```

## <a name="span-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspanspan-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span> 运行 Code Analysis for Drivers 验证函数声明


若要帮助您确定是否准备好的源代码，请运行[Code Analysis for Drivers](code-analysis-for-drivers.md)。 代码分析函数角色类型声明的驱动程序检查并且可以帮助标识可能错过的函数声明或函数定义的参数不匹配函数角色类型中时向您发出警告。

 

 





