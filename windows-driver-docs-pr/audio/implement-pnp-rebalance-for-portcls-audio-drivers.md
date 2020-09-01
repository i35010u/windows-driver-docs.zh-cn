---
title: 为 PortCls 音频驱动程序实现 PnP 再平衡
description: 对于需要重新分配内存资源的某些 PCI 方案，将使用 PnP 重新平衡。
ms.assetid: FCAD7F8B-AA9B-430A-BCAF-04E13FA15382
ms.date: 04/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 10fd014f4573be1592a44cf94e0d27245723d7c4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209119"
---
# <a name="implement-pnp-rebalance-for-portcls-audio-drivers"></a>为 PortCls 音频驱动程序实现 PnP 再平衡


对于需要重新分配内存资源的某些 PCI 方案，将使用 PnP 重新平衡。

可在两种主要方案中触发重新平衡：

1. PCI 热插拔：用户插入设备，PCI 总线没有足够的资源来加载新设备的驱动程序。 属于此类别的设备的一些示例包括闪电、USB-C 和 NVME 存储。 在这种情况下，需要重新排列和合并 (重新平衡) 的内存资源，以支持添加其他设备。
2. PCI resizeable 竖线：在内存中成功加载设备的驱动程序后，它会请求其他资源。 设备的一些示例包括高端图形卡和存储设备。 有关视频驱动程序支持的详细信息，请参阅可 [调整大小的栏支持](../display/resizable-bar-support.md)。
本主题介绍为 PortCls 音频驱动程序实现 PnP 重新平衡需要执行哪些操作。

Windows 10 版本1511及更高版本的 Windows 中提供了 PnP 重新平衡。

## <a name="span-idrebalance_requirementsspanspan-idrebalance_requirementsspanspan-idrebalance_requirementsspanrebalance-requirements"></a><span id="Rebalance_Requirements"></span><span id="rebalance_requirements"></span><span id="REBALANCE_REQUIREMENTS"></span>重新平衡要求


如果满足以下条件，Portcls 音频驱动程序可以支持重新平衡：

-   小型端口必须向 Portcls 注册 [IAdapterPnpManagement](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpnpmanagement) 接口。
-   小型端口必须从 [**IAdapterPnpManagement：： GetSupportedRebalanceType**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-getsupportedrebalancetype)返回 PcRebalanceRemoveSubdevices。
-   拓扑和 WaveRT 是支持的两种端口类型。

若要在有活动的音频流时支持重新平衡，portcls 音频驱动程序需要满足这两项额外要求。

-   驱动程序支持音频流的 [**IMiniportWaveRTInputStream：： GetReadPacket**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket) 和 [IMiniportWaveRTOutputStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertoutputstream) 数据包接口。 这是建议选项。

或

-   如果驱动程序不支持流的 get/write IMiniportWaveRT，则驱动程序不得支持 [**KSPROPERTY \_ RTAUDIO \_ POSITIONREGISTER**](./ksproperty-rtaudio-positionregister.md) 和 [**KSPROPERTY \_ RTAUDIO \_ CLOCKREGISTER**](./ksproperty-rtaudio-clockregister.md)。 在此方案中，音频引擎将使用 [**IMiniportWaveRTStream：： GetPosition**](/previous-versions/windows/hardware/drivers/ff536749(v=vs.85)) 。

## <a name="span-idaudio_stream_behavior_when_rebalancing_occursspanspan-idaudio_stream_behavior_when_rebalancing_occursspanspan-idaudio_stream_behavior_when_rebalancing_occursspanaudio-stream-behavior-when-rebalancing-occurs"></a><span id="Audio_Stream_Behavior_When_Rebalancing_Occurs"></span><span id="audio_stream_behavior_when_rebalancing_occurs"></span><span id="AUDIO_STREAM_BEHAVIOR_WHEN_REBALANCING_OCCURS"></span>发生重新平衡时的音频流行为


如果触发了重新平衡，则当存在活动的音频流并且驱动程序为活动音频流提供支持重新平衡时，所有活动的音频流都将停止，并且不会自动重新启动。

## <a name="span-idiportclspnp_com_interfacespanspan-idiportclspnp_com_interfacespanspan-idiportclspnp_com_interfacespaniportclspnp-com-interface"></a><span id="IPortClsPnp_COM_Interface"></span><span id="iportclspnp_com_interface"></span><span id="IPORTCLSPNP_COM_INTERFACE"></span>IPortClsPnp COM 接口


`IPortClsPnp` 是 PnP 管理接口，端口类驱动程序 (PortCls) 向适配器公开此接口。

`IPortClsPnp` 继承自 **IUnknown** ，还支持以下方法：

-   [**IPortClsPnp::RegisterAdapterPnpManagement**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspnp-registeradapterpnpmanagement)
-   [**IPortClsPnp::UnregisterAdapterPnpManagement**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspnp-unregisteradapterpnpmanagement)

音频微型端口驱动程序可以使用 Portcls 导出或通过 WaveRT 端口对象上公开的 [**IPortClsPnp**](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclspnp) COM 接口 IPORTCLSPNP 注册 PNP 通知接口。 使用 [**IPortClsPnp：： RegisterAdapterPnpManagement**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspnp-registeradapterpnpmanagement) 和 [**IPortClsPnp：： UnregisterAdapterPnpManagement**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclspnp-unregisteradapterpnpmanagement) 注册和注销。

## <a name="span-idrequired_portcls_export_ddisspanspan-idrequired_portcls_export_ddisspanspan-idrequired_portcls_export_ddisspanrequired-portcls-export-ddis"></a><span id="Required_PortCls_Export_DDIs"></span><span id="required_portcls_export_ddis"></span><span id="REQUIRED_PORTCLS_EXPORT_DDIS"></span>必需的 PortCls 导出 DDIs


[IAdapterPnpManagement](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpnpmanagement) 是适配器应该实现并注册的接口，如果要接收 PnP 管理消息。 使用 [**PcRegisterAdapterPnpManagement**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpnpmanagement)将此接口注册到 PortCls。 使用 [**PcUnregisterAdapterPnpManagement**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpnpmanagement)将此接口注册到 PortCls。

## <a name="span-idrequired_driver_ddisspanspan-idrequired_driver_ddisspanspan-idrequired_driver_ddisspanrequired-driver-ddis"></a><span id="Required_Driver_DDIs"></span><span id="required_driver_ddis"></span><span id="REQUIRED_DRIVER_DDIS"></span>必需的驱动程序 DDIs


必须实现以下 [IAdapterPnpManagement](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpnpmanagement) DDIs 以支持重新平衡。

-   [**IAdapterPnpManagement：： GetSupportedRebalanceType**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-getsupportedrebalancetype) 在处理 QueryStop 时由 Portcls 调用。 此微型端口按 [**PC 重新 \_ 平衡 \_ 类型**](/windows-hardware/drivers/ddi/portcls/ne-portcls-pc_rebalance_type) 枚举中定义的方式返回受支持的重新平衡类型。

    **注意**   Portcls 在进行此调用之前获取设备全局锁，因此小型端口必须尽可能快地执行此调用。

     

-   [**IAdapterPnpManagement:P：**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-pnpquerystop) Portcls 在 QueryStop IRP 成功之前调用 npquerystop。 这只是一个通知，并且调用不返回值。

    **注意**   Portcls 在进行此调用之前获取设备全局锁，因此小型端口必须尽可能快地执行此调用。 停止处于挂起状态时，Portcls 将阻止 (保留) 所有新的创建请求。

     

-   [**IAdapterPnpManagement：**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-pnpcancelstop) 在处理 CanceStop IRP 时 portcls 调用:P npcancelstop。 这只是一个通知。 即使在以前未收到 PnpQueryStop 通知的情况下，微型端口也可以接收 PnpCancelStop。 应该写入微型端口来容纳此行为。 例如，如果 QueryStop 逻辑在 Portcls 有机会将此通知转发到小型小型端口之前失败，则会出现这种情况。 在此方案中，PnP 管理器仍会调用 PnP 取消停止。

    **注意**   Portcls 在进行此调用之前获取设备全局锁，因此小型端口必须尽可能快地执行此调用。 停止处于挂起状态时，Portcls 将阻止 (保留) 所有新的创建请求。 取消挂起的停止后，PortCls 将重新启动任何挂起的创建请求。

     

-   [**IAdapterPnpManagement：**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-pnpstop) 在停止所有 Ioctl 操作并将活动流从 \[ 运行 | 暂停 | 获取 \] 状态移动到 \[ 停止状态之后，Portcls 调用:P npstop \] 。 在持有设备全局锁时不进行此调用。 因此，小型端口有机会等待其异步操作 (工作项、dpc、异步线程) 并注销其音频 subdevices。 从此调用返回之前，微型端口必须确保所有的 h/w 资源都已释放。

    **注意**   小型端口不得等待当前微型端口/流对象被删除，因为现有的音频客户端将释放当前句柄。 PnpStop 线程不会在系统崩溃（即 PnP/Power 线程）的情况下永远阻止。

     

## <a name="span-id_iminiportpnpnotifyspanspan-id_iminiportpnpnotifyspanspan-id_iminiportpnpnotifyspan-iminiportpnpnotify"></a><span id="_IMiniportPnpNotify"></span><span id="_iminiportpnpnotify"></span><span id="_IMINIPORTPNPNOTIFY"></span> IMiniportPnpNotify


[IMiniportPnpNotify](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportpnpnotify) 是一个可选接口，用于允许)  (音频 subdevices 的微型端口对象接收 PnP 状态更改通知。

微型端口有机会接收每个注册的音频 subdevice 的 PnP 停止通知。 若要接收此通知，subdevice 必须支持 [IMiniportPnpNotify](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportpnpnotify)。 仅在此接口上定义了 [**IMiniportPnpNotify：:P npstop**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportpnpnotify-pnpstop) 通知。

IMiniportPnpNotify 接口可用于 WaveRT 和拓扑。

**注意**   由于 Portcls 在进行此调用之前获取设备全局锁，因此小型端口必须尽可能快地执行此调用。 当处理此调用时，微型端口不得等待其他活动，以防止其他线程/工作项等待设备全局锁定时出现死锁。 如果需要，可在 IAdapterPnpManagement 中等待的小型小型端口 [**：:P npstop**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpnpmanagement-pnpstop) 调用。