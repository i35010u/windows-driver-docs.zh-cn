---
title: MB SAR 平台支持
description: MB SAR 平台支持
ms.date: 05/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: d604c45320edca15ab45d15bdca157cc35126cf2
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557792"
---
# <a name="mb-sar-platform-support"></a>MB SAR 平台支持

## <a name="overview"></a>概述

传统上，Oem 已经实现了特定的吸收率（SAR）专用解决方案。 这要求 OEM 实现仅在其用户模式驱动程序（UMDF）和调制解调器之间确定的设备服务命令，或者要求内核模式组件直接与调制解调器交互。 某些 Oem 甚至可能会有混合解决方案，在此解决方案中，它们同时具有 UMDF 和内核模式的调制解调器组件。 随着收音机辐射认知的增加，将用于通过 SAR 命令的 OEM 软件组件的接口标准化可带来以下好处：

1.  Oem 可以向用户模式组件移动并使系统更稳定，因为用户模式中的错误与内核模式相比不是致命的。
2.  Windows 提供了平台标准接口，并减少了 Oem 的专有实现。
3.  要利用 SAR 的平台中的服务可以从调制解调器中检索信息。

从 Windows 10 版本1703开始，Windows 支持通过 SAR 配置和调制解调器传输状态。 Windows 将继续将 SAR 业务逻辑留给 Ihv 和 Oem，以将其用作自区分因素，但会提供一个接口来简化平台。 定义了两个新的 NDIS Oid 和两个新的 MBIM Cid 来支持此接口。 需要利用 OS 支持的设备必须实现这两个命令。

通过添加两个新的 Oid 和 Cid，支持此功能。 对于实现 MBIM 的 IHV 合作伙伴，只需支持 CID 版本。

> [!NOTE]
> 本主题定义了用于 IHV 合作伙伴在其调制解调器设备驱动程序中实现 SAR 平台支持的接口。 如果正在寻找有关自定义设备的 SAR 映射表的信息，请参阅[自定义特定的吸收率（SAR）映射表](https://docs.microsoft.com/windows-hardware/customize/desktop/customize-sar-mapping-table)。

## <a name="mb-interface-update-for-sar-platform-support"></a>SAR 平台支持的 MB 接口更新

与 MBIM 兼容的设备在 CID_MBIM_DEVICE_SERVICES 进行查询时实现并报告以下设备服务。 在 USB NCM MBIM 1.0 规范的第10.1 节中定义了现有的已知服务。 Microsoft 对此进行了扩展，定义了以下服务。

服务名称 = **MICROSOFT SAR 控件**

UUID = **UUID_MS_SARControl**

UUID 值 = **68223D04-9F6C-4E0F-822D-28441FB72340**

| CID | 最低操作系统版本 |
| --- | --- |
| MBIM_CID_MS_SAR_CONFIG | Windows 10 版本 1703 |
| MBIM_CID_MS_TRANSMISSION_STATUS | Windows 10 版本 1703 |

## <a name="mbim_cid_ms_sar_config"></a>MBIM_CID_MS_SAR_CONFIG

### <a name="description"></a>说明

此命令设置或返回有关 MB 设备的 SAR 后退模式和级别的信息。 MB 设备必须通过覆盖当前传输功率限制并将它们应用到传输天线来立即操作 SAR 后关闭命令。 如果系统不更改天线的 SAR 配置，则它应保持其当前设置。 例如，如果操作系统将天线1设置为 SAR 反向索引1，则天线2的配置应保持不变，而不进行任何更改。

对于支持此命令的设备，该设备应为实现查询，以便将设备信息提供给操作系统及其客户端。 对于 Set 命令，它位于 IHV 和 OEM 之间，用于定义每个字段的值是可接受的。 典型的期望是，将所有天线的 "SAR 后关闭" 索引配置为最小基线。 如果使用设备不支持的字段发送集请求，则必须以状态代码形式返回 MBIM_STATUS_INVALID_PARAMETERS。

完成每个查询或设置响应后，调制解调器应返回 MBIM_MS_SAR_CONFIG 结构，其中包含与移动宽带关联的设备上所有天线的信息。

#### <a name="query"></a>查询

不使用 MBIM_COMMAND_MSG 上的 InformationBuffer。 MBIM_MS_SAR_CONFIG 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。

#### <a name="set"></a>设置

MBIM_COMMAND_MSG 上的 InformationBuffer 包含 MBIM_MS_SAR_CONFIG。 MBIM_MS_SAR_CONFIG 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。

#### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="parameters"></a>参数

| Operation | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_SET_SAR_CONFIG | 不适用 | 不适用 |
| 响应 | MBIM_MS_SAR_CONFIG | MBIM_MS_SAR_CONFIG | 不适用 |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询

InformationBuffer 应为 NULL，而 InformationBufferLength 应为零。

#### <a name="set"></a>设置

以下 MBIM_MS_SET_SAR_CONFIG 结构应在 InformationBuffer 中使用。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARMode | MBIM_MS_SAR_CONTROL_MODE | 有关详细信息，请参阅 MBIM_MS_SAR_CONTROL_MODE 表。 |
| 4 | 4 | SARBackOffStatus | MBIM_MS_SAR_BACKOFF_STATE | 有关详细信息，请参阅 MBIM_MS_SAR_BACKOFF_STATE 表。  如果 MBIM_MS_SAR_CONTROL_MODE 设置为设备控制的，则 OS 将无法设置此字段。 |
| 8 | 4 | Elementcount 多于（EC） | UINT32 | DataBuffer 中后面的 MBIM_MS_SAR_CONFIG 结构的计数。 |
| 12 | 8 * EC | SARConfigStatusRefList | OL_PAIR_LIST | 该对的第一个元素为4字节的偏移量，该偏移量是从此 MBIM_MS_SET_SAR_CONFIG 结构的开始（偏移量0）计算到 MBIM_MS_SAR_CONFIG_STATE 结构的。 有关详细信息，请参阅 MBIM_MS_SAR_CONFIG_STATE 表。 对的第二个元素是指向相应 MBIM_MS_SAR_CONFIG_STATE 结构的指针的大小为4字节。 |
| 12 + （8 * EC） |  | DataBuffer | DATABUFFER | MBIM_MS_SAR_CONFIG_STATE 结构的数组。 |

前面的表中使用了以下结构。

MBIM_MS_SAR_CONTROL_MODE 指定如何控制 SAR 反向机制。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MBIMMsSARControlModeDevice | 0 | SAR 反向机制由调制解调器设备直接控制。 |
| MBIMMsSARControlModeOS | 1 | SAR 后关闭机制由操作系统控制和管理。 |

MBIM_MS_SAR_BACKOFF_STATE 描述 SAR 返回的状态。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MBIMMsSARBackOffStatusDisabled | 0 | 在调制解调器中禁用了 SAR 后关闭。 |
| MBIMMsSARBackOffStatusEnabled | 1 | 在调制解调器中启用了 SAR 后关闭。 |

MBIM_MS_SAR_CONFIG_STATE 描述了针对天线的 SAR 回退可能的状态。

| Offset | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARAntennaIndex | UINT32 | 与此表中的**SARBackOffIndex**字段相对应的天线索引。 它对应于天线号，并留给 OEM 实现为设备上的每个天线编制索引。 任何索引对于此值都有效。 如果在*set*命令中将此值设置为**0xffffffff** ，则应将**SARBackOffIndex**应用于所有天线。 如果此值设置为 " **0xffffffff** "，则表示**SARBackOffIndex**应用于所有天线。 |
| 4 | 4 | SARBAckOffIndex | UINT32 | 对应于由 OEM 或调制解调器供应商定义的后端表的 "后退" 索引。 该表包含单独的带区和关联的后向外参数。 |

#### <a name="response"></a>响应

以下 MBIM_MS_SAR_CONFIG 结构应在 InformationBuffer 中使用。 MBIM_MS_SAR_CONFIG 指定 SAR 的配置。

| Offset | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARMode | MBIM_MS_SAR_MODE | 有关详细信息，请参阅 MBIM_MS_SAR_CONTROL_MODE 表。 |
| 4 | 4 | SARBackOffStatus | MBIM_MS_SAR_BACKOFF_STATE | 有关详细信息，请参阅 MBIM_MS_SAR_BACKOFF_STATE 表。 |
| 8 | 4 | SARWifiIntegration | MBIM_MS_SAR_ WIFI_HARDWARE_INTEGRATION | 有关详细信息，请参阅 MBIM_MS_SAR_HARDWARE_WIFI_INTEGRATION 表。 这表示设备的 Wi-fi 和移动电话 SAR 在硬件层上集成，并且设备将自动调整两个收音机的 SAR 控件。 |
| 12 | 4 | Elementcount 多于（EC） | UINT32 | DataBuffer 中后面的 MBIM_MS_SAR_CONFIG_STATE 结构的计数。 |
| 16 | 8 * EC | SARConfigStatusRefList | OL_PAIR_LIST | 该对的第一个元素为4字节的偏移量，该偏移量是从该 MBIM_MS_SAR_CONFIG 结构的开始（偏移量0）计算到 MBIM_MS_SAR_CONFIG_STATE 结构的。 有关详细信息，请参阅 MBIM_MS_SAR_CONFIG_STATE 表。 对的第二个元素是指向相应 MBIM_MS_SAR_CONFIG_STATE 结构的指针的大小为4字节。 |
| 16 + （8 * EC） |  | DataBuffer | DATABUFFER | MBIM_MS_SAR_CONFIG_STATE 结构的数组。 |

上表中使用了以下 MBIM_MS_SAR_HARDWARE_WIFI_INTEGRATION 结构。 它指定 Wi-fi 和蜂窝设备是否在硬件级别集成。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MBIMMsSARWifiHardwareIntegrated  | 0 | Wi-fi 和移动电话调制解调器 SAR 已集成到设备中。 |
| MBIMMsSARWifiHardwareNotIntegrated | 1 | Wi-fi 和移动电话调制解调器 SAR 未集成到设备中。 |

#### <a name="notification"></a>通知

不适用。

### <a name="status-codes"></a>状态代码

| 错误代码 | 说明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 已成功处理请求。 |
| MBIM_STATUS_BUSY | 设备当前正忙。 |
| MBIM_STATUS_FAILURE | 请求失败。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 设备不支持此命令。 |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_OPERATION_NOT_ALLOWED | 操作失败，因为不允许该操作。 |

## <a name="mbim_cid_ms_transmission_status"></a>MBIM_CID_MS_TRANSMISSION_STATUS

### <a name="description"></a>说明

此命令用于启用或禁用传输状态下的调制解调器发出的通知。 它是按执行器命令，因为每个执行器可以具有不同的通道传输状态。 例如，两个 SIM 卡上可能有一个用于 LTE 的，另一个是 GSM 上的另一个调制解调器。 同时，可以使用它来提供调制解调器的传输状态。 此通知可用于对调制解调器是否正在传输数据感兴趣的客户端。 每当存在开始或结束的 TX 流量时，调制解调器应提供通知。 如果该税种周期太小并且无法实时地提供给主机，则在发送状态更新之前，TX 状态可以保持为活动状态，具有滞后时间计时器。 例如，可能会有一段时间发生短暂的 TX，并且调制解调器无法及时提供开始和结束通知。 当 TX 流量开始时，该调制解调器应发送通知，并且应在滞后计时器期间继续监视其 TX 流量。 如果在计时器的时间范围内没有生成更多的 TX 流量，则会报告 TX 流量已结束。

这在连接了 Wi-fi 和 LTE 的方案中非常有用。  如果 LTE 和 Wi-fi 都处于传输状态，并且检测到邻近状态，则可能需要 Wi-fi 后退。 如果 LTE 未处于传输状态，但 Wi-fi 为，则可能不需要 Wi-fi 后退。 这适用于常规 Wi-fi/LTE 连接和移动热点方案。  

Wi-fi 后关闭机制和命令超出了此规范。 

使用此命令的 Oem 应注意到可能的电源影响，因为调制解调器可能始终发送与传输相关的通知，其中包括减少的电源状态。 默认情况下，OS 不会允许此通知在新式备用期间唤醒 AP，以提高电源性能。

#### <a name="query"></a>查询

不使用 MBIM_COMMAND_MSG 上的 InformationBuffer。 MBIM_MS_TRANSMISSION_STATUS_INFO 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。

#### <a name="set"></a>设置

MBIM_COMMAND_MSG 上的 InformationBuffer 包含 MBIM_MS_SET_TRANSMISSION_STATUS。 MBIM_MS_TRANSMISSION_STATUS_INFO 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。

#### <a name="unsolicited-events"></a>未经请求的事件

未经请求的事件包含 MBIM_MS_TRANSMISSION_STATUS_INFO 并在发生活动的无线（OTA）通道发生更改时发送。 例如，如果调制解调器开始上传数据包数据，则需要在使用网络数据通道时设置上行通道，以便能够上传有效负载。 这会触发向操作系统提供通知。

### <a name="parameters"></a>参数

| Operation | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_SET_TRANSMISSION_STATUS | 不适用 | 不适用 |
| 响应 | MBIM_MS_TRANSMISSION_STATUS_INFO | MBIM_MS_TRANSMISSION_STATUS_INFO | MBIM_MS_TRANSMISSION_STATUS_INFO |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询

不使用 MBIM_COMMAND_MSG 上的 InformationBuffer。 MBIM_MS_TRANSMISSION_STATUS_INFO 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。 

#### <a name="set"></a>设置

以下 MBIM_MS_SET_TRANSMISSION_STATUS 结构应在 InformationBuffer 中使用。

| Offset | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ChannelNotification | MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION | 有关详细信息，请参阅 MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION 表。 |
| 4 | 4 | HysteresisTimer | UINT32 | 用于确定何时将 MBIMMsTransmissionStateInactive 发送到主机的滞后指示器。 此值是调制解调器在向主机发送 OFF 指示器之前视为连续无传输活动的计时器。 此计时器应以秒为单位进行设置，范围介于1秒到5秒之间。 |

上表中使用了以下 MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION 结构。 它指定调制解调器通道传输是否已禁用或启用。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MBIMMsTransmissionNotificationDisabled | 0 | 调制解调器通道传输状态通知已禁用。 |
| MBIMMsTransmissionNotificationEnabled | 1 | 调制解调器通道传输状态通知已启用。 |

#### <a name="response"></a>响应

以下 MBIM_MS_TRANSMISSION_STATUS_INFO 结构用于响应。

| Offset | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ChannelNotification | MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION | 有关详细信息，请参阅 MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION 表。 |
| 4 | 4 | TransmissionStatus | MBIM_MS_TRANSMISSION_STATUS | 有关详细信息，请参阅 MBIM_MS_TRANSMISSION_STATUS 表。 这表明调制解调器每5秒钟是否有 TX 流量。 |
| 8 | 4 | HysteresisTimer | UINT32 | 用于确定何时将 MBIMMsTransmissionStateInactive 发送到主机的滞后指示器。 此值是调制解调器在向主机发送 OFF 指示器之前视为连续无传输活动的计时器。 此计时器应以秒为单位进行设置，范围介于1秒到5秒之间。 |

上表中使用了以下 MBIM_MS_TRANSMISSION_STATUS 结构。 它指示调制解调器每5秒钟是否有 TX 流量。

| 类型 | 值 | 描述 |
| --- | --- | --- |
| MBIMMsTransmissionStateInactive | 0 | 对于最后的 HysteresisTimer 值，调制解调器不会主动传输数据，无需任何持续传输。 |
| MBIMMsTransmissionStateActive | 1 | 调制解调器正在主动传输数据。 |

#### <a name="notification"></a>通知

有关详细信息，请参阅 MBIM_MS_TRANSMISSION_STATUS_INFO 表。

### <a name="status-codes"></a>状态代码

| 错误代码 | 说明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 已成功处理请求。 |
| MBIM_STATUS_BUSY | 设备当前正忙。 | 
| MBIM_STATUS_FAILURE | 请求失败。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 设备不支持此命令。 |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_OPERATION_NOT_ALLOWED | 操作失败，因为不允许该操作。 |


