---
title: MB SAR 平台支持
description: MB SAR 平台支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36d29378af0b76c3c3e664b75e82ad5e0c8e9313
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353757"
---
# <a name="mb-sar-platform-support"></a>MB SAR 平台支持

## <a name="overview"></a>概述

一直以来，Oem 已实现专有解决方案特定吸收速率 （特别行政区）。 这要求实现设备服务命令或者仅标识其用户模式驱动程序 (UMDF) 和调制解调器之间或需要内核模式组件，以便直接与调制解调器的 OEM。 某些 Oem 甚至提供了混合解决方案必须 UMDF 调制解调器和内核模式调制解调器组件。 由于已增加单选放射意识，标准化为 OEM 软件组件，以通过特别行政区命令传递到调制解调器接口引入了以下优势：

1.  Oem 可以将移动用户模式组件的趋势，并且会使系统更稳定，因为用户模式下的错误不是致命的系统与内核模式的比较。
2.  Windows 提供了平台标准接口，并减少来自 Oem 的专有实现。
3.  想要利用特别行政区在平台中的服务可以从调制解调器检索信息。

从 Windows 10，版本 1703，Windows 支持通过特别行政区配置和调制解调器传输状态传递。 Windows 将继续保留为用作自区别因素 Ihv 和 Oem 特别行政区业务逻辑，但将提供一个界面，用于简化平台。 已定义两个新的 NDIS Oid 和两个新 MBIM Cid，来支持此接口。 想要利用操作系统支持的设备必须实现这两个命令。

通过添加两个新的 Oid 和 Cid 中支持此功能。 实现 MBIM 的 IHV 合作伙伴，只会将 CID 版本需要受支持。

> [!NOTE]
> 本主题定义 IHV 合作伙伴在其调制解调器设备驱动程序中实现特别行政区平台支持的接口。 如果您正在寻找有关自定义设备特别行政区映射表的信息，请参阅[自定义特定吸收速率 （特别行政区） 映射表](https://docs.microsoft.com/windows-hardware/customize/desktop/customize-sar-mapping-table)。

## <a name="mb-interface-update-for-sar-platform-support"></a>有关特别行政区平台支持 MB 界面更新

MBIM 合规的设备实现，并报告以下设备服务 CID_MBIM_DEVICE_SERVICES 进行查询时。 10.1 一部分 USB NCM MBIM 1.0 规范中定义现有的已知服务。 Microsoft 扩展，以便定义以下服务。

服务名称 = **Microsoft 特别行政区控件**

UUID = **UUID_MS_SARControl**

UUID Value = **68223D04-9F6C-4E0F-822D-28441FB72340**

| CID | 最低 OS 版本 |
| --- | --- |
| MBIM_CID_MS_SAR_CONFIG | Windows 10 版本 1703 |
| MBIM_CID_MS_TRANSMISSION_STATUS | Windows 10 版本 1703 |

## <a name="mbimcidmssarconfig"></a>MBIM_CID_MS_SAR_CONFIG

### <a name="description"></a>描述

此命令设置或返回退避模式和级别的 MB 设备的特别行政区有关的信息。 MB 设备必须立即执行操作上退避命令特别行政区通过覆盖当前传输 power 限制并将其应用于传输的天线。 如果不天线的特别行政区配置进行了更改的操作系统，它应保持其当前设置。 例如，如果操作系统设置天线 1 退避为特别行政区索引 1，然后天线 2 的配置应保持不变而不进行任何更改。

它应支持以下命令来实现查询，因此，它们提供设备信息的 OS 和其客户端的设备。 对于 Set 命令，它是之间 IHV 和 OEM 定义的每个字段的值是可接受。 典型的预期结果是退避索引特别行政区作为最小基准是可配置用于所有天线。 如果 Set 请求发送与设备不支持的字段，则必须为状态代码返回 MBIM_STATUS_INVALID_PARAMETERS。

每个查询或一组响应后, 调制解调器应返回 MBIM_MS_SAR_CONFIG 结构，其中包含与移动宽带关联的设备上所有天线的信息。

#### <a name="query"></a>查询

不使用上 MBIM_COMMAND_MSG InformationBuffer。 MBIM_MS_SAR_CONFIG MBIM_COMMAND_DONE InformationBuffer 中返回。

#### <a name="set"></a>设置

在 MBIM_COMMAND_MSG InformationBuffer 包含 MBIM_MS_SAR_CONFIG。 MBIM_MS_SAR_CONFIG MBIM_COMMAND_DONE InformationBuffer 中返回。

#### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_MS_SET_SAR_CONFIG | 不适用 | 不适用 |
| 响应 | MBIM_MS_SAR_CONFIG | MBIM_MS_SAR_CONFIG | 不适用 |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询

InformationBuffer 应为 NULL，并且将 InformationBufferLength 应该为零。

#### <a name="set"></a>设置

应在 InformationBuffer 中使用以下 MBIM_MS_SET_SAR_CONFIG 结构。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARMode | MBIM_MS_SAR_CONTROL_MODE | 有关详细信息，请参阅 MBIM_MS_SAR_CONTROL_MODE 表。 |
| 4 | 4 | SARBackOffStatus | MBIM_MS_SAR_BACKOFF_STATE | 有关详细信息，请参阅 MBIM_MS_SAR_BACKOFF_STATE 表。  如果 MBIM_MS_SAR_CONTROL_MODE 是集是设备控制的则操作系统将不能设置此字段。 |
| 8 | 4 | ElementCount (EC) | UINT32 | 按照中 DataBuffer MBIM_MS_SAR_CONFIG 计数结构。 |
| 12 | 8 * EC | SARConfigStatusRefList | OL_PAIR_LIST | 该对的第一个元素是 4 字节的偏移量，从一开始 （偏移量为 0） 的此 MBIM_MS_SET_SAR_CONFIG 结构，计算到 MBIM_MS_SAR_CONFIG_STATE 结构。 有关详细信息，请参阅 MBIM_MS_SAR_CONFIG_STATE 表。 该对的第二个元素是指针的指向相应 MBIM_MS_SAR_CONFIG_STATE 结构的 4 字节大小。 |
| 12 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_SAR_CONFIG_STATE 结构的数组。 |

前面的表中使用以下结构。

MBIM_MS_SAR_CONTROL_MODE 指定如何控制特别行政区回退机制。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMMsSARControlModeDevice | 0 | 特别行政区退让机制直接控制通过调制解调器设备。 |
| MBIMMsSARControlModeOS | 1 | 特别行政区退让机制是控制和管理的操作系统。 |

MBIM_MS_SAR_BACKOFF_STATE 退避介绍特别行政区的状态。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMMsSARBackOffStatusDisabled | 0 | 返回特别行政区 off 中禁用了调制解调器。 |
| MBIMMsSARBackOffStatusEnabled | 1 | 返回特别行政区 off 中启用了调制解调器。 |

MBIM_MS_SAR_CONFIG_STATE 介绍特别行政区退避算法的天线的可能状态。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARAntennaIndex | UINT32 | 对应于天线指数**SARBackOffIndex**此表中的字段。 它对应于天线数，并为从左到 OEM 实现，以在设备上的每个天线的索引。 此值的任何索引无效。 如果此值设置为**0xFFFFFFFF**中*设置*命令， **SARBackOffIndex**应应用于所有天线。 如果此值设置为**0xFFFFFFFF**在响应中，它表明**SARBackOffIndex**应用于所有天线。 |
| 4 | 4 | SARBAckOffIndex | UINT32 | 答： 退避对应于退避由 OEM 或调制解调器供应商定义的表的索引。 此表有单个带区和关联的退避参数。 |

#### <a name="response"></a>响应

应在 InformationBuffer 中使用以下 MBIM_MS_SAR_CONFIG 结构。 MBIM_MS_SAR_CONFIG 指定特别行政区的配置。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARMode | MBIM_MS_SAR_MODE | 有关详细信息，请参阅 MBIM_MS_SAR_CONTROL_MODE 表。 |
| 4 | 4 | SARBackOffStatus | MBIM_MS_SAR_BACKOFF_STATE | 有关详细信息，请参阅 MBIM_MS_SAR_BACKOFF_STATE 表。 |
| 8 | 4 | SARWifiIntegration | MBIM_MS_SAR_ WIFI_HARDWARE_INTEGRATION | 有关详细信息，请参阅 MBIM_MS_SAR_HARDWARE_WIFI_INTEGRATION 表。 这意味着在硬件层集成设备的 Wi-fi 和移动电话特别行政区，设备会自动调整为这两个无线电收发器特别行政区控件。 |
| 12 | 4 | ElementCount (EC) | UINT32 | 按照中 DataBuffer MBIM_MS_SAR_CONFIG_STATE 计数结构。 |
| 16 | 8 * EC | SARConfigStatusRefList | OL_PAIR_LIST | 该对的第一个元素是一个 4 字节偏移量，从一开始 （偏移量为 0） 的此 MBIM_MS_SAR_CONFIG 结构，计算到 MBIM_MS_SAR_CONFIG_STATE 结构。 有关详细信息，请参阅 MBIM_MS_SAR_CONFIG_STATE 表。 该对的第二个元素是指针的指向相应 MBIM_MS_SAR_CONFIG_STATE 结构的 4-字节大小。 |
| 16 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_SAR_CONFIG_STATE 结构的数组。 |

前面的表中使用以下 MBIM_MS_SAR_HARDWARE_WIFI_INTEGRATION 结构。 它指定是否在硬件级别集成的 Wi-fi 和移动电话。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMMsSARWifiHardwareIntegrated  | 0 | Wi-fi 和移动电话调制解调器特别行政区被集成到设备中。 |
| MBIMMsSARWifiHardwareNotIntegrated | 1 | Wi-fi 和移动电话调制解调器特别行政区未集成到设备中。 |

#### <a name="notification"></a>通知

不适用。

### <a name="status-codes"></a>状态代码

| 错误代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 已成功处理该请求。 |
| MBIM_STATUS_BUSY | 设备是当前正忙。 |
| MBIM_STATUS_FAILURE | 请求失败。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 设备不支持此命令。 |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_OPERATION_NOT_ALLOWED | 操作失败，因为不允许的操作。 |

## <a name="mbimcidmstransmissionstatus"></a>MBIM_CID_MS_TRANSMISSION_STATUS

### <a name="description"></a>描述

此命令用于启用或禁用从调制解调器的通知上传输状态。 它是每个执行器命令，因为每个执行器可以具有不同的通道传输状态。 例如，双 SIM 调制解调器可能有上 GSM 上 LTE，另一个。 同时，它可以用于提供调制解调器的传输状态。 无法对是否调制解调器正在传输数据，或不感兴趣的客户端使用此通知。 调制解调器应提供任何时间没有开始或结束 TX 流量的通知。 如果占空比太小，无法向主机提供实时，然后 TX 状态可以保留为活动状态设置时间滞后计时器与之前发送的状态更新。 例如，可能会遇到的 TX 短突然增加，调制解调器无法提供时间中的开始和结束通知。 调制解调器应 TX 流量启动时发送通知以及是否应继续在滞后计时器期间监视其 TX 流量。 如果没有更多的 TX 流量在计时器的时间段内生成时，它应该报告 TX 流量已结束。

这是在连接的 Wi-fi 和 LTE 的情况中非常有用。  如果检测到邻近 LTE 和 Wi-fi 处于传输状态，然后 Wi-fi 回 off 可能需要。 如果 LTE 不在传输状态但 Wi-fi，那么 Wi-fi 后退可能不需要。 这适用于一般 Wi-Fi/LTE 连接和移动热点方案。  

此规范的范围超出了 Wi-fi 退让机制和命令。 

使用此命令的 Oem 应注意 power 造成的潜在影响可能会在所有时间，包括减少了的电源状态与传输相关的通知发送调制解调器。 OS，默认情况下，将不允许此通知以在新式待机状态来改善电源唤醒 AP。

#### <a name="query"></a>查询

不使用上 MBIM_COMMAND_MSG InformationBuffer。 MBIM_MS_SET_TRANSMISSION_STATUS_INFO MBIM_COMMAND_DONE InformationBuffer 中返回。

#### <a name="set"></a>设置

在 MBIM_COMMAND_MSG InformationBuffer 包含 MBIM_MS_SET_TRANSMISSION_STATUS。 MBIM_MS_SET_TRANSIMISSION_STATUS _INFO MBIM_COMMAND_DONE InformationBuffer 中返回。

#### <a name="unsolicited-events"></a>未经请求的事件

未经请求的事件包含 MBIM_MS_TRANSMISSION_STATUS_INFO 和活动的无线 (OTA) 通道到更改时发送。 例如，如果调制解调器开始上传数据包数据，它所需设置上行通道时它使用的网络数据通道，以便它可以上传有效负载。 这将触发该通知可提供给操作系统。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_MS_SET_TRANSMISSION_STATUS | 不适用 | 不适用 |
| 响应 | MBIM_MS_TRANSMISSION_STATUS_INFO | MBIM_MS_TRANSMISSION_STATUS_INFO | MBIM_MS_TRANSMISSION_STATUS_INFO |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询

不使用上 MBIM_COMMAND_MSG InformationBuffer。 MBIM_MS_TRANSMISSION_STATUS_INFO MBIM_COMMAND_DONE InformationBuffer 中返回。 

#### <a name="set"></a>设置

应在 InformationBuffer 中使用以下 MBIM_MS_SET_TRANSMISSION_STATUS 结构。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ChannelNotification | MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION | 有关详细信息，请参阅 MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION 表。 |
| 4 | 4 | HysteresisTimer | UINT32 | 调制解调器用于确定何时向主机发送 MBIMMsTransmissionStateInactive 滞后指标。 此值是连续否-发送活动 OFF 指标发送到主机之前，会看到调制解调器的计时器。 以秒为单位，范围从 1 秒到 5 秒，应设置此计时器。 |

前面的表中使用以下 MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION 结构。 它指定是否禁用或启用调制解调器通道传输。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMMsTransmissionNotificationDisabled | 0 | 禁用调制解调器通道传输状态通知。 |
| MBIMMsTransmissionNotificationEnabled | 1 | 启用调制解调器通道传输状态通知。 |

#### <a name="response"></a>响应

以下 MBIM_MS_TRANSMISSION_STATUS_INFO 结构用于响应。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ChannelNotification | MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION | 有关详细信息，请参阅 MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION 表。 |
| 4 | 4 | TransmissionStatus | MBIM_MS_TRANSMISSION_STATUS | 有关详细信息，请参阅 MBIM_MS_TRANSMISSION_STATUS 表。 这指示是否调制解调器具有 TX 流量每隔 5 秒。 |
| 8 | 4 | HysteresisTimer | UINT32 | 调制解调器用于确定何时向主机发送 MBIMMsTransmissionStateInactive 滞后指标。 此值是连续否-发送活动 OFF 指标发送到主机之前，会看到调制解调器的计时器。 以秒为单位，范围从 1 秒到 5 秒，应设置此计时器。 |

前面的表中使用以下 MBIM_MS_TRANSMISSION_STATUS 结构。 它指示是否调制解调器有 TX 流量每隔 5 秒。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMMsTransmissionStateInactive | 0 | 调制解调器不主动传输了数据，而不传输的最后一个 HysteresisTimer 值任何连续失效。 |
| MBIMMsTransmissionStateActive | 1 | 调制解调器已主动传输数据。 |

#### <a name="notification"></a>通知

有关详细信息，请参阅 MBIM_MS_SET_TRANSMISSION_STATUS_INFO 表。

### <a name="status-codes"></a>状态代码

| 错误代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 已成功处理该请求。 |
| MBIM_STATUS_BUSY | 设备是当前正忙。 | 
| MBIM_STATUS_FAILURE | 请求失败。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 设备不支持此命令。 |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_OPERATION_NOT_ALLOWED | 操作失败，因为不允许的操作。 |


