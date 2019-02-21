---
title: HFP 设备启动
description: HFP 设备启动本主题将讨论蓝牙免提配置文件 (HFP) 设备到达音频系统中时，会发生什么情况。
ms.assetid: C478BCBA-2A17-4604-AE2B-99B3445C741B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13434323205ff001db3eb1105ecfd2c5817ed878
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546253"
---
# <a name="hfp-device-startup"></a>HFP 设备启动


HFP 设备启动本主题将讨论蓝牙免提配置文件 (HFP) 设备到达音频系统中时，会发生什么情况。

对于每个配对的 HFP 设备的直接音频系统，Windows HFP 驱动程序注册设备接口的 guid\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 类。 音频驱动程序使用设备接口通知以了解最新信息的所有实例的 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 接口。 音频驱动程序调用 IoRegisterPlugPlayNotification 从其 AVStrMiniDevicePostStart 驱动程序例程中 （或等效的 Portcls 例程） 来注册一个回调以发现的当前安装的 HFP 设备，并接收通知的新 HFP 设备。

当音频驱动程序调用 IoRegisterPlugPlayNotification 时，使用以下参数进行调用。

-   EventCategory 设置为 EventCategoryDeviceInterfaceChange。

-   EventCategoryFlags 通常设置为 PNPNOTIFY\_设备\_界面\_INCLUDE\_现有\_为了接收即时通知现有接口的接口。 但是一些备用的音频驱动程序设计可能会发现通过其他方式的现有接口。

-   EventCategoryData 设置为 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS。

-   DriverObject 设置为音频驱动程序的 DriverObject。

-   CallbackRoutine 设置为将接收通知的音频驱动程序中的例程。

以下部分概述的任务的音频驱动程序可以执行的每个已注册实例配对 HFP 设备。

## <a name="span-idhandlinginterfaceinstancesspanspan-idhandlinginterfaceinstancesspanspan-idhandlinginterfaceinstancesspanhandling-interface-instances"></a><span id="Handling_interface_instances"></span><span id="handling_interface_instances"></span><span id="HANDLING_INTERFACE_INSTANCES"></span>处理接口实例


在 GUID 中注册每个接口实例的\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 类音频驱动程序必须使用以下协议进行通信：

当 Windows 调用音频驱动程序调用 IoRegisterPlugPlayNotification 时已注册的音频驱动程序的回调例程时，Windows 将传递 HFP 接口的符号链接使用的设备\_接口\_更改\_通知。*SymbolicLinkName*。

当音频驱动程序调用 IoGetDeviceObjectPointer 时，驱动程序将使用符号链接以获取 HFP 文件对象和 HFP 设备 DeviceObject。

当音频驱动程序将 Ioctl 发送到 HFP 驱动程序时，驱动程序使用 HFP 文件对象和 DeviceObject HFP 设备。

## <a name="span-idretrievingstaticinformationspanspan-idretrievingstaticinformationspanspan-idretrievingstaticinformationspanretrieving-static-information"></a><span id="Retrieving_static_information"></span><span id="retrieving_static_information"></span><span id="RETRIEVING_STATIC_INFORMATION"></span>检索静态信息


音频驱动程序可以从 HFP 驱动程序检索静态信息。 例如，HFP 驱动程序可以提供 ksnodetype、 容器 id 和配对 HFP 设备的友好名称。 音频驱动程序可以使用此信息来创建和初始化 KS 筛选器或筛选器表示配对的 HFP 设备。 音频驱动程序将使用[ **IOCTL\_BTHHFP\_设备\_获取\_描述符**](https://msdn.microsoft.com/library/windows/hardware/dn265108)来获取此信息。

音频驱动程序还可以检索配对 HFP 设备的蓝牙地址。 每个配对的 HFP 设备有一个唯一的蓝牙地址，，这可用作唯一标识符字符串。 有关详细信息，请参阅[HF 设备蓝牙获取地址](obtaining-bluetooth-address-of-hf-device.md)。

## <a name="span-idcreatinginitializingaudio-specificfilterfactorycontextspanspan-idcreatinginitializingaudio-specificfilterfactorycontextspanspan-idcreatinginitializingaudio-specificfilterfactorycontextspancreating-initializing-audio-specific-filter-factory-context"></a><span id="Creating__initializing_audio-specific_filter_factory_context"></span><span id="creating__initializing_audio-specific_filter_factory_context"></span><span id="CREATING__INITIALIZING_AUDIO-SPECIFIC_FILTER_FACTORY_CONTEXT"></span>创建、 初始化特定于音频的筛选器工厂上下文


若要创建和初始化特定于音频的筛选器工厂上下文，音频驱动程序必须将 HFP DeviceObject 和 HFP 文件对象存储在筛选器工厂上下文，然后 IsConnected 字段初始化为 false。

## <a name="span-idcreatingtheksfilterfactoryspanspan-idcreatingtheksfilterfactoryspanspan-idcreatingtheksfilterfactoryspancreating-the-ks-filter-factory"></a><span id="Creating_the_KS_filter_factory"></span><span id="creating_the_ks_filter_factory"></span><span id="CREATING_THE_KS_FILTER_FACTORY"></span>创建 KS 筛选器工厂


中每个设备实例 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 接口类，音频驱动程序创建并启用一个或多个筛选器工厂。

如果音频驱动程序，AVStream 驱动程序音频驱动程序调用 KsCreateFilterFactory 添加新的筛选器工厂和 KsFilterFactorySetDeviceClassesState 启用工厂。 如果音频驱动程序是一个 PortCls 驱动程序，然后它间接创建并通过调用 PcRegisterSubdevice 使 KS 筛选器工厂。 对于许多 PortCls 音频驱动程序设计有两个子设备为给定的配对 HFP 设备注册。

每个筛选器工厂 （或者，对于 PortCls 音频驱动程序，每个对筛选器工厂） 表示单个配对 HFP 设备的音频功能。 音频驱动程序创建单独的筛选器工厂的 GUID 的唯一实例所表示的每个配对 HFP 设备\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 接口。 对于每个配对的 HFP 设备，音频驱动程序必须使用唯一字符串*RefString* KsCreateFilterFactory，参数或*名称*PcRegisterSubdevice 参数。 驱动程序开发人员可能会发现可以使用配对的 HFP 设备的蓝牙地址字符串作为唯一字符串。 请参阅[HF 设备蓝牙获取地址](obtaining-bluetooth-address-of-hf-device.md)有关如何检索的唯一字符串的信息。

请注意，没有任何特定设备数上限可能配对 HFP，因此音频驱动程序应避免在硬编码特定的限制。 相反，音频驱动程序必须正确处理动态到达和删除多个 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 接口。

在实践中，但是，PortCls 驱动程序必须指定子设备的最大数目时，它调用 PcAddAdapterDevice。 PcAddAdapterDevice 预分配额外内存用于每个潜在子设备。 音频驱动程序开发人员应选择一个足够高以适应多个配对的设备，但一次选择一种资源浪费在不会产生一个数字的数字。 例如，支持只有 2 个 HFP 设备可能是不够的并且支持 2000年肯定导致过度扩张的资源。 但是，支持 16 很可能是合理。

如果在运行时的音频驱动程序通知的另一个 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 接口，但已注册了其最大数量的子设备，则音频驱动程序可以调用某些算法，用于选择配对的 HFP 设备取消注册它可以为新的 HFP 设备腾出空间，请其子设备。 例如，音频驱动程序无法跟踪的 HFP 设备与最早的连接。 而更简单但可能小于用户友好的音频驱动程序可能只需忽略其他 GUID\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 接口后达到其最大值。

## <a name="span-idsendingthegetconnectionstatusioctlspanspan-idsendingthegetconnectionstatusioctlspanspan-idsendingthegetconnectionstatusioctlspansending-the-get-connection-status-ioctl"></a><span id="Sending_the_get_connection_status_IOCTL"></span><span id="sending_the_get_connection_status_ioctl"></span><span id="SENDING_THE_GET_CONNECTION_STATUS_IOCTL"></span>发送 get 连接状态 IOCTL


音频驱动程序将发送 get 连接状态 IOCTL，以获取有关在连接中发生的任何更改的信息。

## <a name="span-idsendingthegetvolumestatusioctlspanspan-idsendingthegetvolumestatusioctlspanspan-idsendingthegetvolumestatusioctlspansending-the-get-volume-status-ioctl"></a><span id="Sending_the_get_volume_status_IOCTL"></span><span id="sending_the_get_volume_status_ioctl"></span><span id="SENDING_THE_GET_VOLUME_STATUS_IOCTL"></span>发送 get 卷状态 IOCTL


音频驱动程序将发送 get 卷状态 IOCTL，若要获取中音量级别中的耳机该卷的状态已发生的任何更改的信息。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题
[**IOCTL\_BTHHFP\_DEVICE\_GET\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/dn265108)  
[理论上的操作](theory-of-operation.md)  
[获取 HF 设备的蓝牙地址](obtaining-bluetooth-address-of-hf-device.md)  



