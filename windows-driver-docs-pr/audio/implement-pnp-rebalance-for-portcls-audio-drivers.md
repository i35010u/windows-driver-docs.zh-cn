---
title: 为 PortCls 音频驱动程序实现 PnP 再平衡
description: 即插即用重新平衡是方案中使用某些 PCI 需要重新分配内存资源。
ms.assetid: FCAD7F8B-AA9B-430A-BCAF-04E13FA15382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d0881661fb05211711bfcb13845fd748293d7fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333487"
---
# <a name="implement-pnp-rebalance-for-portcls-audio-drivers"></a>为 PortCls 音频驱动程序实现 PnP 再平衡


即插即用重新平衡是方案中使用某些 PCI 需要重新分配内存资源。

可以在两个主要方案中触发再平衡：

1. PCI 热插拔：用户插入设备和 PCI 总线不具有足够的资源来加载新设备的驱动程序。 属于此类别的设备的一些示例包括闪电、 USB C 和 NVME 存储。 在此方案中内存资源需要重新排列和合并 (rebalanced) 以支持要添加的其他设备。
2. PCI 可调整其大小栏：设备的驱动程序已成功加载到内存中后，它请求的其他资源。 设备的一些示例包括高端的图形卡和存储设备。 有关视频驱动程序支持，请参阅详细信息[可调整大小栏支持](https://msdn.microsoft.com/library/windows/hardware/dn894179)。
本主题介绍需要做的目的在于实现 PnP 重新平衡 PortCls 音频驱动程序的内容。

即插即用重新平衡是在 Windows 10，版本 1511年和更高版本的 Windows 中可用。

## <a name="span-idrebalancerequirementsspanspan-idrebalancerequirementsspanspan-idrebalancerequirementsspanrebalance-requirements"></a><span id="Rebalance_Requirements"></span><span id="rebalance_requirements"></span><span id="REBALANCE_REQUIREMENTS"></span>重新平衡要求


Portcls 音频驱动程序能够支持重新平衡，如果满足以下条件：

-   微型端口必须注册[IAdapterPnpManagement](https://msdn.microsoft.com/library/windows/hardware/mt604850) Portcls 接口。
-   微型端口必须返回从 PcRebalanceRemoveSubdevices [ **IAdapterPnpManagement::GetSupportedRebalanceType**](https://msdn.microsoft.com/library/windows/hardware/mt604851)。
-   拓扑和 WaveRT 是支持的两个端口类型。

为了支持重新平衡活动音频流时，需要满足以下两个额外要求之一 portcls 音频驱动程序。

-   驱动程序支持[ **IMiniportWaveRTInputStream::GetReadPacket** ](https://msdn.microsoft.com/library/windows/hardware/dn946533)并[IMiniportWaveRTOutputStream](https://msdn.microsoft.com/library/windows/hardware/dn946534)音频流的数据包接口。 这是建议选项。

或者

-   如果该驱动程序不支持 get/写 IMiniportWaveRT 对于流，该驱动程序必须支持[ **KSPROPERTY\_RTAUDIO\_POSITIONREGISTER** ](https://msdn.microsoft.com/library/windows/hardware/ff537381)和[ **KSPROPERTY\_RTAUDIO\_CLOCKREGISTER**](https://msdn.microsoft.com/library/windows/hardware/ff537376)。 音频引擎将使用[ **IMiniportWaveRTStream::GetPosition** ](https://msdn.microsoft.com/library/windows/hardware/ff536749)在此方案中。

## <a name="span-idaudiostreambehaviorwhenrebalancingoccursspanspan-idaudiostreambehaviorwhenrebalancingoccursspanspan-idaudiostreambehaviorwhenrebalancingoccursspanaudio-stream-behavior-when-rebalancing-occurs"></a><span id="Audio_Stream_Behavior_When_Rebalancing_Occurs"></span><span id="audio_stream_behavior_when_rebalancing_occurs"></span><span id="AUDIO_STREAM_BEHAVIOR_WHEN_REBALANCING_OCCURS"></span>音频 Stream 行为重新平衡发生时


如果触发再平衡时，当有活动的音频流，并驱动程序提供支持重新平衡为活动音频流，然后将停止所有活动音频流并不将自动重新。

## <a name="span-idiportclspnpcominterfacespanspan-idiportclspnpcominterfacespanspan-idiportclspnpcominterfacespaniportclspnp-com-interface"></a><span id="IPortClsPnp_COM_Interface"></span><span id="iportclspnp_com_interface"></span><span id="IPORTCLSPNP_COM_INTERFACE"></span>IPortClsPnp COM 接口


`IPortClsPnp` 是即插即用的端口类驱动程序 (PortCls) 公开给适配器的管理接口。

`IPortClsPnp` 继承自**IUnknown** ，并且还支持以下方法：

-   [**IPortClsPnp::RegisterAdapterPnpManagement**](https://msdn.microsoft.com/library/windows/hardware/mt604860)
-   [**IPortClsPnp::UnregisterAdapterPnpManagement**](https://msdn.microsoft.com/library/windows/hardware/mt604861)

音频的微型端口驱动程序可以注册使用 Portcls 导出的即插即用通知接口或通过[ **IPortClsPnp** ](https://msdn.microsoft.com/library/windows/hardware/mt604859) IPortClsPnp WaveRT port 对象上公开的 COM 接口。 使用[ **IPortClsPnp::RegisterAdapterPnpManagement** ](https://msdn.microsoft.com/library/windows/hardware/mt604860)并[ **IPortClsPnp::UnregisterAdapterPnpManagement** ](https://msdn.microsoft.com/library/windows/hardware/mt604861)注册和取消注册。

## <a name="span-idrequiredportclsexportddisspanspan-idrequiredportclsexportddisspanspan-idrequiredportclsexportddisspanrequired-portcls-export-ddis"></a><span id="Required_PortCls_Export_DDIs"></span><span id="required_portcls_export_ddis"></span><span id="REQUIRED_PORTCLS_EXPORT_DDIS"></span>所需的 PortCls 导出 DDIs


[IAdapterPnpManagement](https://msdn.microsoft.com/library/windows/hardware/mt604850)是一个接口，适配器应该实现和注册如果用户想要接收即插即用管理消息。 注册此接口使用 PortCls [ **PcRegisterAdapterPnpManagement**](https://msdn.microsoft.com/library/windows/hardware/mt604865)。 取消注册此接口使用 PortCls [ **PcUnregisterAdapterPnpManagement**](https://msdn.microsoft.com/library/windows/hardware/mt604866)。

## <a name="span-idrequireddriverddisspanspan-idrequireddriverddisspanspan-idrequireddriverddisspanrequired-driver-ddis"></a><span id="Required_Driver_DDIs"></span><span id="required_driver_ddis"></span><span id="REQUIRED_DRIVER_DDIS"></span>必需的驱动程序 DDIs


以下[IAdapterPnpManagement](https://msdn.microsoft.com/library/windows/hardware/mt604850) DDIs 必须实现以支持重新平衡。

-   [**IAdapterPnpManagement::GetSupportedRebalanceType** ](https://msdn.microsoft.com/library/windows/hardware/mt604851) Portcls 处理查询防止时调用。 微型端口返回支持重新平衡类型中定义[ **PC\_重新平衡\_类型**](https://msdn.microsoft.com/library/windows/hardware/mt604867)枚举。

    **请注意**  Portcls 进行此调用之前获取设备全局锁，因此将微型端口必须执行此调用尽可能快。

     

-   [**IAdapterPnpManagement::PnpQueryStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604853) portcls 成功查询防止 IRP 之前调用。 这只是一个通知，并且在调用不返回值。

    **请注意**  Portcls 进行此调用之前获取设备全局锁，因此将微型端口必须执行此调用尽可能快。 Portcls 停止挂起时，将阻止 （按住） 任何新创建的请求。

     

-   [**IAdapterPnpManagement::PnpCancelStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604852) portcls 处理 CanceStop IRP 时调用。 这是只是一个通知。 很可能微型端口，以便即使没有以前接收 PnpQueryStop 通知接收 PnpCancelStop。 应编写微型端口，以适应此行为。 例如，这是这种情况时查询防止逻辑之前发生了故障 IRP Portcls 有机会将转发到微型端口此通知。 在此方案中 PnP 管理器将仍调用即插即用取消停止。

    **请注意**  Portcls 进行此调用之前获取设备全局锁，因此将微型端口必须执行此调用尽可能快。 Portcls 停止挂起时，将阻止 （按住） 任何新创建的请求。 PortCls 重启取消挂起停止时，任何挂起创建请求。

     

-   [**IAdapterPnpManagement::PnpStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604854) Portcls 后停止所有 Ioctl 操作和移动从活动流中调用\[运行 | 暂停 | 获取\]状态变为\[停止\]状态。 不进行此调用，同时保留设备的全局锁定。 因此微型端口，必须等待其异步操作 （工作项、 dpc，异步线程） 和注销其音频子设备的机会。 从此调用返回前微型端口必须确保已发布的所有硬件资源。

    **请注意**  微型端口必须不等待当前的微型端口/流对象，若要删除，因为现有的音频客户端将释放当前句柄时，不清楚。 PnpStop 线程不能永久阻止而不发生崩溃系统，即，这是 PnP/电源线程。

     

## <a name="span-idiminiportpnpnotifyspanspan-idiminiportpnpnotifyspanspan-idiminiportpnpnotifyspan-iminiportpnpnotify"></a><span id="_IMiniportPnpNotify"></span><span id="_iminiportpnpnotify"></span><span id="_IMINIPORTPNPNOTIFY"></span> IMiniportPnpNotify


[IMiniportPnpNotify](https://msdn.microsoft.com/library/windows/hardware/mt604855)一可选接口，以允许微型端口对象 （音频子设备） 可以接收即插即用的状态更改通知。

微型端口，可以接收的即插即用停止通知每个音频子已注册。 若要接收此通知，子必须支持[IMiniportPnpNotify](https://msdn.microsoft.com/library/windows/hardware/mt604855)。 仅[ **IMiniportPnpNotify::PnpStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604856)此接口上定义通知。

WaveRT 和拓扑是 IMiniportPnpNotify 接口可用。

**请注意**  因为 Portcls 进行此调用之前获取设备全局锁、 微型端口必须尽快执行此调用。 微型端口必须处理此调用，以防止其他线程/工作项正在等待设备全局锁时出现死锁时不等待其他活动。 如果需要微型端口中可以等待[ **IAdapterPnpManagement::PnpStop** ](https://msdn.microsoft.com/library/windows/hardware/mt604854)调用。

 

 

 




