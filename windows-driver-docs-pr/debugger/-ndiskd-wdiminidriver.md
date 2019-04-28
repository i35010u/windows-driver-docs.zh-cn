---
title: ndiskd.wdiminidriver
description: Ndiskd.wdiminidriver 扩展显示有关一个或多个 CMiniportDriver 结构的信息。
ms.assetid: C7022CD7-6F3A-485B-8686-A686A5305DA5
keywords:
- ndiskd.wdiminidriver Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.wdiminidriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 90eb2e802ad7357e27ccadfb1a9cb97e447c7d9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335860"
---
# <a name="ndiskdwdiminidriver"></a>!ndiskd.wdiminidriver


**！ Ndiskd.wdiminidriver**扩展显示有关一个或多个 CMiniportDriver 结构的信息。 如果不带任何参数运行此扩展 ！ ndiskd 将显示所有 CMiniportDriver 结构的列表。

有关 WDI 微型端口驱动程序的详细信息，请参阅[WDI 微型端口驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/wdi-miniport-driver-design-guide)。

WDI 微型端口驱动程序引用的详细信息，请参阅[WDI 微型端口驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/dn926075)。

```console
!ndiskd.wdiminidriver [-handle <x>] [-pm] [-rcvfilter] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
CMiniportDriver 对象的句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
显示有关微型端口驱动程序的基本信息。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-handlers*   
显示此驱动程序微型端口处理程序。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd.wdiminidriver**扩展不带任何参数，以查看所有 CMiniportDriver 对象的列表。 在以下示例中，只有一个 CMiniportDriver 对象时。 其 WdiMiniDriver 的句柄是 ffffc804b8ce7c40。

```console
1: kd> !ndiskd.wdiminidriver
    WdiMiniDriver      Name                                                     
    ffffc804b8ce7c40 - WDI MiniDriver
```

单击 WdiMiniDriver 的句柄或输入 **！ ndiskd.wdiminidriver-处理**命令来查看此 WDI 微型端口驱动程序的详细信息。

```console
1: kd> !ndiskd.wdiminidriver ffffc804b8ce7c40


WDI MINIPORT DRIVER

    Object             ffffc804b8ce7c40
    DRIVER_OBJECT      ffffc804b90a4ac0

    Ndis API version   v6.50
    NDIS driver        ffffc804af2e3710 - mrvlpcie8897
    Driver version     v1.0
    WDI API version    v1.0.1


    Handlers
```

现在可以单击 WDI 微型端口驱动程序的详细信息，底部的"处理程序"链接，也可以使用该句柄以输入 **！ ndiskd.wdiminidriver-处理的处理程序**命令，以查看所有此 WDI 微型端口驱动程序的处理程序的列表。

```console
1: kd> !ndiskd.wdiminidriver ffffc804b8ce7c40 -handlers


HANDLERS

    Miniport Handler                       Function pointer   Symbol (if available)
    InitializeHandlerEx                    [None]
    SetOptionsHandler                      fffff80965e8cae0   mrvlpcie8897!wlan_cmd_queue_deinit
    UnloadHandler                          fffff80965e71a08   mrvlpcie8897!MPUnload
    HaltHandlerEx                          [None]
    ShutdownHandlerEx                      fffff80965e71974   mrvlpcie8897!MPShutdown

    CheckForHangHandlerEx                  [None]
    ResetHandlerEx                         [None]

    PauseHandler                           [None]
    RestartHandler                         [None]

    OidRequestHandler                      [None]
    SendNetBufferListsHandler              [None]
    ReturnNetBufferListsHandler            [None]
    CancelSendHandler                      [None]
    CancelOidRequestHandler                [None]
    DirectOidRequestHandler                [None]
    CancelDirectOidRequestHandler          [None]
    DevicePnPEventNotifyHandler            fffff80965e71868   mrvlpcie8897!MPPnPEventNotify

    AllocateAdapterHandler                 fffff80965e713ec   mrvlpcie8897!MPAllocateTalAdapter
    FreeAdapterHandler                     fffff80965e717e8   mrvlpcie8897!MPFreeTalAdapter
    OpenAdapterHandler                     fffff80965e719b8   mrvlpcie8897!MPTaskOpenHandler
    CloseAdapterHandler                    fffff80965e719ac   mrvlpcie8897!MPTaskCloseHandler
    StartOperationHandler                  [None]
    StopOperationHandler                   [None]
    PostPauseHandler                       [None]
    PostRestartHandler                     [None]
    HangDiagnoseHandler                    fffff80965e715d8   mrvlpcie8897!MPDiagnosticHandler
    TalTxRxInitializeHandler               fffff80965e752d4   mrvlpcie8897!TalDataPathInitialize
    TalTxRxDeinitializeHandler             fffff80965e7527c   mrvlpcie8897!TalDataPathDeinitialize

    OpenAdapterCompleteHandler             fffff80965ffab50   wdiwifi!WDIOpenAdapterCompleteHandler
    CloseAdapterCompleteHandler            fffff80965fface0   wdiwifi!WDICloseAdapterCompleteHandler
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[WDI 微型端口驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/wdi-miniport-driver-design-guide)

[WDI 微型端口驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/dn926075)

 

 






