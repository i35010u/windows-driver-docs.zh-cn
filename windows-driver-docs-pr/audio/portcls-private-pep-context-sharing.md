---
title: PortCls 专用 PEP 上下文共享
description: 从 Windows 8 开始，微型端口驱动程序可以共享与 Windows 电源引擎插件 (PEP) 的专用上下文使用 IPortClsRuntimePower，一个新的接口。
ms.assetid: 27A0DD72-8AD0-4F38-B17C-9BDD63C5E7E1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60275cf4760644fe40a1bbed72d31936fdde7b21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362553"
---
# <a name="portcls-private-pep-context-sharing"></a>PortCls 专用 PEP 上下文共享


从 Windows 8 开始，微型端口驱动程序可以共享与 Windows 电源引擎插件 (PEP) 的专用上下文使用 IPortClsRuntimePower，一个新的接口。

音频端口类驱动程序 (PortCls) 已更新，以将新接口，IPortClsRuntimePower WaveRT 端口上公开。 为了使微型端口驱动程序将发送到操作系统的 PEP 的专用 power 控件，微型端口驱动程序首先必须获取到其关联的端口的 IPortClsRuntimePower 接口的访问权限。 然后，微型端口驱动程序注册的回调，在调用适当的时间，从而允许要发送的专用 power 控件的微型端口驱动程序。

## <a name="span-idaccessingiportclsruntimepowerspanspan-idaccessingiportclsruntimepowerspanspan-idaccessingiportclsruntimepowerspanaccessing-iportclsruntimepower"></a><span id="Accessing_IPortClsRuntimePower"></span><span id="accessing_iportclsruntimepower"></span><span id="ACCESSING_IPORTCLSRUNTIMEPOWER"></span>Accessing IPortClsRuntimePower


微型端口驱动程序可以访问其端口 IPortClsRuntimePower 通过以下事件序列：

1. 微型端口驱动程序调用[ **PcNewPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewport)并提供 IID\_为 REFID IPortWaveRT。

2. **PcNewPort**创建类型的端口接口 (Pport) [IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavert)。

3. 微型端口驱动程序中新创建然后调用 QueryInterface **IPortWaveRT**端口接口，并指定 IID\_IPortClsRuntimePower 作为接口的 GUID。

4. **IPortWaveRT**端口接口提供了用一个指针指向的微型端口驱动程序及其[ **IPortClsRuntimePower** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsruntimepower)接口。

*Portcls.h*标头文件的 IPortClsRuntimePower 定义 GUID，如下所示：

``` syntax
// {E057C351-0430-4DBC-B172-C711D40A2373}
DEFINE_GUID(IID_IPortClsRuntimePower,
0xe057c351, 0x430, 0x4dbc, 0xb1, 0x72, 0xc7, 0x11, 0xd4, 0xa, 0x23, 0x73);
```

## <a name="span-idregisteringacallbackspanspan-idregisteringacallbackspanspan-idregisteringacallbackspanregistering-a-callback"></a><span id="Registering_a_callback"></span><span id="registering_a_callback"></span><span id="REGISTERING_A_CALLBACK"></span>注册一个回调


微型端口驱动程序将使用[ **IPortClsRuntimePower::RegisterPowerControlCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsruntimepower-registerpowercontrolcallback)要注册一个回调方法。 当 PEP 启动专用的请求，或启动的微型端口驱动程序本身的专用请求的响应中调用此方法。 虽然该驱动程序处理 IRP，通常应执行回调注册\_MN\_启动\_设备 PNP Irp。

除了回调中提供的上下文指针，其他参数的定义的运行时电源框架 PowerControlCallback 相同定义。 此外，微型端口的回调必须属于类型 PCPFNRUNTIME\_电源\_控制\_回调中的以下代码段定义*Portcls.h*标头文件。

```ManagedCPlusPlus
typedef
NTSTATUS
_IRQL_requires_max_(DISPATCH_LEVEL)
(*PCPFNRUNTIME_POWER_CONTROL_CALLBACK)
(
    _In_        LPCGUID PowerControlCode,
    _In_opt_    PVOID   InBuffer,
    _In_        SIZE_T  InBufferSize,
    _Out_opt_   PVOID   OutBuffer,
    _In_        SIZE_T  OutBufferSize,
    _Out_opt_   PSIZE_T BytesReturned,
    _In_opt_    PVOID   Context
);
```

当停止或删除驱动程序时，它必须使用[ **IPortClsRuntimePower::UnregisterPowerControlCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsruntimepower-unregisterpowercontrolcallback)方法来注销任何已注册的回调。

## <a name="span-idsendingprivatepowercontrolsspanspan-idsendingprivatepowercontrolsspanspan-idsendingprivatepowercontrolsspansending-private-power-controls"></a><span id="Sending_private_power_controls"></span><span id="sending_private_power_controls"></span><span id="SENDING_PRIVATE_POWER_CONTROLS"></span>发送专用电源控制


微型端口建立访问后**IPortClsRuntimePower**接口，并使用该接口的**RegisterPowerControlCallback**方法注册回调，它现在已准备好发送专用电源控制。 微型端口驱动程序调用的回调方法时，使用[ **IPortClsRuntimePower::SendPowerControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsruntimepower-sendpowercontrol)方法以将私有电源控制发送到 Windows PEP。

除*DeviceObject*参数，所有其他参数具有相同定义与运行时电源框架[PoFxPowerControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxpowercontrol)方法。

 

 




