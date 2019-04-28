---
title: ndiskd.oid
description: Ndiskd.oid 扩展显示有关 NDIS OID 请求的信息。
ms.assetid: FCDE2F78-98C0-4437-999A-4566FEB5D7BB
keywords:
- ndiskd.oid Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.oid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4d13728dd646a86dd7bd32073a0886142beb6c77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335908"
---
# <a name="ndiskdoid"></a>!ndiskd.oid


**！ Ndiskd.oid**扩展显示有关 NDIS OID 请求的信息。 如果不带任何参数运行此扩展 ！ ndiskd 将显示有关所有微型端口和筛选器的所有挂起的 OID 请求的列表。 每个微型端口或筛选器具有最多一个挂起 OID 的请求和任意数量的排队 OID 请求。

请注意，筛选器通常克隆 OID 请求，将向下传递克隆。 这意味着，即使是协议发出单个 OID 请求时，可能有多个实例的克隆请求： 一个在每个筛选器，微型端口中的另一个。 **！ ndiskd.oid**分开，将显示每个克隆，因此可能会看到多个挂起的 Oid 不是实际发出协议。

```console
!ndiskd.oid [-handle <x>] [-legacyoid] [-nolimit>] [-miniport <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
句柄的 NDIS\_OID\_请求

<span id="_______-legacyoid______"></span><span id="_______-LEGACYOID______"></span> *-legacyoid*   
将视为旧 NDIS\_请求而不是 NDIS\_OID\_请求。

<span id="_______-nolimit______"></span><span id="_______-NOLIMIT______"></span> *-nolimit*   
不限制显示的 Oid 挂起的次数。

<span id="_______-miniport______"></span><span id="_______-MINIPORT______"></span> *-miniport*   
查找挂起的 OID 请求此微型端口堆栈上。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>备注
-------

**！ ndiskd.oid**显示列表的所有挂起的 Oid 在系统上一次，因此它可以帮助调试系统挂起或[0x9F bug 检查](https://msdn.microsoft.com/library/windows/hardware/ff559329)的情况下 (驱动程序\_POWER\_状态\_失败)。 例如，假设分析的虚构 0x9F bug 检查揭示系统已挂起上 IRP，正在等待 NDIS。 在 NDIS，从操作系统的 Irp 将转换为 Oid，包括电源转换，因此，通过运行 **！ ndiskd.oid**大家可以看到，在此示例中，堆栈的底部处的设备可能已被一堆到[OID\_PNP\_设置\_电源](https://msdn.microsoft.com/library/windows/hardware/ff569780)和挂起堆栈的其余部分。 NDIS 驱动程序应该不挂起 OID 对超过一秒，以便可以然后调查为什么该设备保留太长时间挂起的 OID 来尝试解决该问题。

<a name="examples"></a>示例
--------

若要正常运行的系统上查看挂起的 OID 的示例，请 （在微型端口的相应微型端口驱动程序） 的微型端口的 OID 请求处理程序例程上设置断点。 首先，运行[ **！ ndiskd.minidriver** ](-ndiskd-minidriver.md)命令不带任何参数来获取系统上的微型端口驱动程序的列表。 在此示例输出中，查找为句柄 kdnic 微型驱动程序，ffffdf801418d650...

```console
3: kd> !ndiskd.minidriver
    ffffdf8015a98380 - tunnel
    ffffdf801418d650 - kdnic
```

单击句柄上的微型驱动程序，然后单击其详细信息页面以查看其处理程序的列表底部的"处理程序"链接。 或者，可以输入 **！ ndiskd.minidriver-处理的处理程序**命令。 微型驱动程序的处理程序的列表后，查找其句柄，在此示例中的 fffff80f1fd71c90 OidRequestHandler。

```console
2: kd> !ndiskd.minidriver ffffdf801418d650 -handlers


HANDLERS

    NDIS Handler                           Function pointer   Symbol (if available)
    InitializeHandlerEx                    fffff80f1fd78230  bp
    SetOptionsHandler                      fffff80f1fd72800  bp
    HaltHandlerEx                          fffff80f1fd78040  bp
    ShutdownHandlerEx                      fffff80f1fd722c0  bp

    CheckForHangHandlerEx                  fffff80f1fd72810  bp
    ResetHandlerEx                         fffff80f1fd72f70  bp

    PauseHandler                           fffff80f1fd78000  bp
    RestartHandler                         fffff80f1fd78940  bp

    OidRequestHandler                      fffff80f1fd71c90  bp
    CancelOidRequestHandler                fffff80f1fd722c0  bp
    DirectOidRequestHandler                [None]
    CancelDirectOidRequestHandler          [None]
    DevicePnPEventNotifyHandler            fffff80f1fd789a0  bp

    SendNetBufferListsHandler              fffff80f1fd71870  bp
    ReturnNetBufferListsHandler            fffff80f1fd71b50  bp
    CancelSendHandler                      fffff80f1fd722c0  bp
```

现在，单击"最佳实践"OidRequestHandler 右侧链接，或输入[**最佳实践-处理**](bp--bu--bm--set-breakpoint-.md)命令和其句柄，该例程上设置断点。 接下来，键入**g**命令，以允许在调试对象目标计算机以运行并命中断点只需设置。

```console
2: kd> bp fffff80f1fd71c90
2: kd> g
Breakpoint 1 hit
fffff80f`1fd71c90 448b4204        mov     r8d,dword ptr [rdx+4]
```

一旦已触发微型驱动程序的 OID 请求处理程序例程上的断点，如上面的示例所示，可以运行 ！ ndiskd.oid 命令，列出在系统上的所有挂起的 Oid。

```console
1: kd> !ndiskd.oid


ALL PENDING OIDs

    NetAdapter         ffffdf80140c71a0 - Microsoft Kernel Debug Network Adapter
        Current OID        OID_GEN_STATISTICS
    Filter             ffffdf8014950c70 - Microsoft Kernel Debug Network Adapter-WFP Native MAC Layer LightWeight Filter-0000
        Current OID        OID_GEN_STATISTICS
    Filter             ffffdf801494dc70 - Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000
        Current OID        OID_GEN_STATISTICS
```

在此示例中，是挂起的 OID [OID\_代\_统计信息](https://msdn.microsoft.com/library/windows/hardware/ff569640)。 当您查看的结果 ！ ndiskd.oid，回想一下，筛选器克隆 OID 请求并将其传递堆栈的下层，和 Oid 通常传递筛选器来筛选到微型端口。 因此，尽管它可能看上去是有三个单独的 OID 请求具有相同名称在此示例中，但没有实际一个逻辑操作发生是以物理方式分布在 3 个 Oid 和对 3 个的驱动程序。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[0x9F bug 检查](https://msdn.microsoft.com/library/windows/hardware/ff559329)

[OID\_PNP\_SET\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)

[**最佳实践，bu，bm （设置断点）**](bp--bu--bm--set-breakpoint-.md)

[OID\_GEN\_STATISTICS](https://msdn.microsoft.com/library/windows/hardware/ff569640)

[NDIS Oid](https://msdn.microsoft.com/library/windows/hardware/ff566707)

[NDIS OID 请求接口](https://msdn.microsoft.com/library/windows/hardware/ff566713)

 

 






