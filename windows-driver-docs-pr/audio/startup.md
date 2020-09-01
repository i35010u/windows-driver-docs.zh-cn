---
title: HFP 设备启动
description: HFP 设备启动主题讨论当) 设备在音频系统中出现时，蓝牙免提配置文件 (HFP 发生了什么情况。
ms.assetid: C478BCBA-2A17-4604-AE2B-99B3445C741B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6a608dd4bb005051f077248fa95cab2799b6c62
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210363"
---
# <a name="hfp-device-startup"></a>HFP 设备启动


HFP 设备启动主题讨论当) 设备在音频系统中出现时，蓝牙免提配置文件 (HFP 发生了什么情况。

对于到达音频系统的每个配对的 HFP 设备，Windows HFP 驱动程序在 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 类中注册了一个设备接口。 音频驱动程序使用设备接口通知随时了解 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 接口的所有实例。 音频驱动程序从其 AVStrMiniDevicePostStart 驱动程序例程 (或从等效的 Portcls 例程) 中调用 IoRegisterPlugPlayNotification，以注册一个回调以发现当前已安装的 HFP 设备，并通知新的 HFP 设备。

当音频驱动程序调用 IoRegisterPlugPlayNotification 时，使用以下参数发出调用。

-   EventCategory 设置为 EventCategoryDeviceInterfaceChange。

-   通常将 EventCategoryFlags 设置为 PNPNOTIFY \_ 设备 \_ 接口 \_ 包含 \_ 现有 \_ 接口，以便接收现有接口的即时通知。 但有些备用音频驱动程序设计可能会通过其他方式找到现有接口。

-   EventCategoryData 设置为 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS。

-   DriverObject 设置为音频驱动程序的 DriverObject。

-   CallbackRoutine 设置为将接收通知的音频驱动程序中的例程。

以下部分概述了音频驱动程序可以为成对 HFP 设备的每个已注册实例执行的任务。

## <a name="span-idhandling_interface_instancesspanspan-idhandling_interface_instancesspanspan-idhandling_interface_instancesspanhandling-interface-instances"></a><span id="Handling_interface_instances"></span><span id="handling_interface_instances"></span><span id="HANDLING_INTERFACE_INSTANCES"></span>处理接口实例


对于在 GUID DEVINTERFACE 蓝牙 HFP SCO HCIBYPASS 类中注册的每个接口实例 \_ \_ \_ \_ \_ ，音频驱动程序必须使用以下协议进行通信：

当 Windows 调用在音频驱动程序调用 IoRegisterPlugPlayNotification 时注册的音频驱动程序的回调例程时，Windows 将使用设备 \_ 接口更改通知为 HFP 接口传递符号 \_ 链接 \_ 。*SymbolicLinkName*。

当音频驱动程序调用 Plxntb 时，驱动程序将使用符号链接获取 HFP 设备的 HFP FileObject 和 DeviceObject。

当音频驱动程序将 IOCTLs 发送到 HFP 驱动程序时，驱动程序将使用 HFP FileObject，并为 HFP 设备使用 DeviceObject。

## <a name="span-idretrieving_static_informationspanspan-idretrieving_static_informationspanspan-idretrieving_static_informationspanretrieving-static-information"></a><span id="Retrieving_static_information"></span><span id="retrieving_static_information"></span><span id="RETRIEVING_STATIC_INFORMATION"></span>检索静态信息


音频驱动程序可以从 HFP 驱动程序检索静态信息。 例如，HFP 驱动程序可以提供 ksnodetype、容器 id 和配对 HFP 设备的友好名称。 音频驱动程序可以使用此信息来创建和初始化一个 KS 筛选器，或代表配对的 HFP 设备的筛选器。 音频驱动程序使用 [**IOCTL \_ BTHHFP \_ 设备 \_ get \_ 描述符**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor) 获取此信息。

音频驱动程序还可以检索配对 HFP 设备的蓝牙地址。 每个配对的 HFP 设备都具有唯一的蓝牙地址，这可用作唯一标识符字符串。 有关详细信息，请参阅 [获取 HF 设备的蓝牙地址](obtaining-bluetooth-address-of-hf-device.md)。

## <a name="span-idcreating__initializing_audio-specific_filter_factory_contextspanspan-idcreating__initializing_audio-specific_filter_factory_contextspanspan-idcreating__initializing_audio-specific_filter_factory_contextspancreating-initializing-audio-specific-filter-factory-context"></a><span id="Creating__initializing_audio-specific_filter_factory_context"></span><span id="creating__initializing_audio-specific_filter_factory_context"></span><span id="CREATING__INITIALIZING_AUDIO-SPECIFIC_FILTER_FACTORY_CONTEXT"></span>创建、初始化特定于音频的筛选器工厂上下文


若要创建并初始化特定于音频的筛选器工厂上下文，音频驱动程序必须在筛选器工厂上下文中存储 HFP DeviceObject 和 HFP FileObject，然后将 Connectionmultiplexer.isconnected 字段初始化为 false。

## <a name="span-idcreating_the_ks_filter_factoryspanspan-idcreating_the_ks_filter_factoryspanspan-idcreating_the_ks_filter_factoryspancreating-the-ks-filter-factory"></a><span id="Creating_the_KS_filter_factory"></span><span id="creating_the_ks_filter_factory"></span><span id="CREATING_THE_KS_FILTER_FACTORY"></span>创建 KS 筛选器工厂


对于 GUID \_ DEVINTERFACE \_ BLUETOOTH HFP SCO HCIBYPASS 接口类中的每个设备实例 \_ \_ \_ ，音频驱动程序将创建并启用一个或多个筛选器工厂。

如果音频驱动程序是 AVStream 驱动程序，则音频驱动程序会调用 KsCreateFilterFactory 来添加新的筛选器工厂和 KsFilterFactorySetDeviceClassesState，以启用工厂。 如果音频驱动程序是 PortCls 驱动程序，则它会通过调用 PcRegisterSubdevice 间接创建并启用 KS 筛选器工厂。 对于许多 PortCls 音频驱动程序设计，有两个子设备注册到了一台给定的配对 HFP 设备。

每个筛选器工厂 (或者，对于 PortCls 音频驱动程序，每对筛选器工厂) 表示单个配对 HFP 设备的音频功能。 音频驱动程序为每个配对的 HFP 设备创建单独的筛选器工厂，由 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 接口的唯一实例表示。 对于每个配对的 HFP 设备，音频驱动程序必须对 KsCreateFilterFactory 的 *RefString* 参数或 PcRegisterSubdevice 的 *Name* 参数使用唯一字符串。 驱动程序开发人员可能会发现，将配对的 HFP 设备的蓝牙地址字符串用作唯一字符串会很有用。 有关如何检索唯一字符串的信息，请参阅 [获取 HF 设备的蓝牙地址](obtaining-bluetooth-address-of-hf-device.md) 。

请注意，没有特定数量的可能配对 HFP 设备，因此音频驱动程序应避免对特定限制进行硬编码。 相反，音频驱动程序必须正确处理多个 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 接口的动态到达和删除。

但是，在实际情况下，PortCls 驱动程序在调用 PcAddAdapterDevice 时必须指定最大数量的子设备。 PcAddAdapterDevice 为每个可能的子设备预分配额外的内存。 音频驱动程序开发人员应选择一个足以容纳多个配对设备的数字，但同时选择不会导致资源浪费的数字。 例如，仅支持2个 HFP 设备可能不满足需要，而支持2000则肯定会导致 overextended 的资源。 但是，支持16可能是合理的。

如果在运行时向音频驱动程序通知另一个 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 接口，但已注册其最大子设备数，则音频驱动程序可以调用一种算法来选择配对的 HFP 设备，该设备的子设备可以取消注册以便为新的 HFP 设备腾出空间。 例如，音频驱动程序可以跟踪具有最旧连接的 HFP 设备。 虽然更简单，但用户友好的音频驱动程序在 \_ \_ \_ \_ \_ 达到其最大值后，可能只是忽略其他 GUID DEVINTERFACE 蓝牙 HFP SCO HCIBYPASS 接口。

## <a name="span-idsending_the_get_connection_status_ioctlspanspan-idsending_the_get_connection_status_ioctlspanspan-idsending_the_get_connection_status_ioctlspansending-the-get-connection-status-ioctl"></a><span id="Sending_the_get_connection_status_IOCTL"></span><span id="sending_the_get_connection_status_ioctl"></span><span id="SENDING_THE_GET_CONNECTION_STATUS_IOCTL"></span>发送 get 连接状态 IOCTL


音频驱动程序发送 get 连接状态 IOCTL，以获取有关连接中发生的任何更改的信息。

## <a name="span-idsending_the_get_volume_status_ioctlspanspan-idsending_the_get_volume_status_ioctlspanspan-idsending_the_get_volume_status_ioctlspansending-the-get-volume-status-ioctl"></a><span id="Sending_the_get_volume_status_IOCTL"></span><span id="sending_the_get_volume_status_ioctl"></span><span id="SENDING_THE_GET_VOLUME_STATUS_IOCTL"></span>发送获取卷状态 IOCTL


音频驱动程序发送 "获取卷状态" IOCTL，以获取有关在头戴式耳机的卷状态中发生的任何卷级更改的信息。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[**IOCTL \_ BTHHFP \_ 设备 \_ 获取 \_ 描述符**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)  
[操作理论](theory-of-operation.md)  
[获取 HF 设备的蓝牙地址](obtaining-bluetooth-address-of-hf-device.md)