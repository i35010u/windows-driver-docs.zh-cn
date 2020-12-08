---
title: 使用 DSS 进行 MB 调制解调器日志记录
description: 使用 DSS 进行 MB 调制解调器日志记录
keywords:
- MB 的调制解调器日志记录，具有 dss 的移动宽带调制解调器日志记录
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3e398c9b3f40a3067baa8fbf642d31f8cbadacfc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841181"
---
# <a name="mb-modem-logging-with-dss"></a>使用 DSS 进行 MB 调制解调器日志记录

## <a name="overview"></a>概述

本主题介绍了一种新的标准 Windows mobile 宽带 (MBB) 日志记录接口，该接口通过 Microsoft extension to the USB MBIM 1.0 规格，适用于 Windows 10，版本1903及更高版本。 

使用这一新的日志记录接口，操作系统可以通过 MBIM CID 命令通知 MBB 设备启动、停止和刷新 OS 文件系统。 由于调制解调器的日志记录负载的非 IP 性质，MBB 服务用来将日志记录负载传输到 OS 的数据通道使用 MBB 数据服务流 (DSS) 。 在 [移动宽带接口模型中定义了 DSS (MBIM) 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip) 规范。 

操作系统使用一组特定于 Windows 的 MBB 日志记录配置，在整个 MBB 生态系统中对调制解调器的诊断功能和配置进行抽象化。 通过这些 MBB 日志记录配置，调制解调器的供应商可将 OS MBB 日志记录需求映射到适当的内部日志记录配置。 操作系统抽象并定义的日志记录配置包括 MBB 日志记录详细级别和最大刷新时间。 

在 (达到最大缓冲区大小并且 MBIM 框架将段传输到 OS 之前，或在达到最大刷新时间时刷新其缓冲区的内容时，即使未) 填充段，调制解调器仍会完全填充其日志记录缓冲区。 操作系统定义一组标准的 Windows MBB 日志记录配置级别，本主题稍后将对此进行介绍。 每个配置级别指定 MBB 日志记录详细信息和详细级别的操作系统抽象。

MBB 配置级别的操作系统抽象通过调制解调器映射到适当的内部调制解调器配置。 操作系统不会将任何其他配置负载（如日志筛选器或掩码）提供给除 OS MBB 配置级别以外的调制解调器。 

对于支持 MBB 日志记录的调制解调器，所有 BSP 变量上都必须存在除 MBIMLoggingLevelOem 之外的所有 MBB 日志记录配置级别。 换句话说，IHV 或 OEM 必须在生产和 R&D 版本的 BSP 中支持生产或实验室级别的 MBB 日志记录。 只能从操作系统禁用 MBB 日志记录的实验室级别。

这一新的日志记录接口设计使用控制通道来设置日志记录参数，并使用数据通道接收调制解调器日志，因为数据通道旨在传输大容量的调制解调器数据。 此设计的优点是不需要通过控制通道传输大容量数据，从而使设备性能保持一致。 它还可以很好地进行缩放，以提高吞吐量。 数据通道由 DSS 命令操作。 调制解调器的示例流可能如下所示：

1. OS 将 MBIM_CID_MODEM_LOGGING_CONFIG CID 发送到调制解调器，以配置日志记录参数，如 MaxSegmentSize、MaxFlushTime 和 Logginglevel.information。
2. 一旦 OS 接收到调制解调器的成功响应后，它会将 MBIM_CID_DSS_CONNECT DSS 命令发送到带有特定 GUID 的调制解调器日志记录、MBIMDssLinkActivate 状态和唯一的 DSS 会话 ID。
3. 收到成功状态代码后，操作系统将准备从调制解调器接收片段。 这些碎片称为 DataServiceSessionRead 的数据包。
4. DataServiceSessionRead 数据包将继续到达，直到操作系统颁发另一个 MBIM_CID_DSS_CONNECT 命令，该命令具有相同的 DSS 会话 ID 和 MBIMDSSLinkDeactivate 状态。

## <a name="modem-logging-data-path"></a>调制解调器日志记录数据路径

Moddem 日志记录使用 MBIM 数据服务流 (DSS) 传输数据以记录负载。 有关 DSS 的详细信息，请参阅 [MBIM 1.0 规范](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的10.5.38 部分。 

从 DSS 连接或断开连接时，会将以下 GUID 用于调制解调器日志记录：

| GUID | “值” |
| --- | --- |
| ModemFileTransfer GUID | 0EBB1CEB-AF2D-484D-8DF3-53BC51FD162C |

以下流程图说明了 DSS 设置和关闭过程。

![DSS 调制解调器日志设置和细分流关系图](images/mb-modem-logging-dss-flow.png "DSS 调制解调器日志记录设置并拆下流关系图。")

## <a name="ndis-interface-extension"></a>NDIS 接口扩展

在 Windows 10 版本1903中定义了以下 OID 以支持调制解调器日志记录。

- [OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)

## <a name="mbim-service-and-cid-values"></a>MBIM 服务和 CID 值

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft 基本 IP 连接扩展插件 | UUID_BASIC_CONNECT_EXTENSIONS | 3d01dcc5-fef5-4d05-9d3a-bef7058e9aaf |

下表指定了每个 CID 的 UUID 和命令代码，以及该 CID 是否支持 Set、Query 或 Event (通知) 请求。 有关其参数、数据结构和通知的详细信息，请参阅本主题中的每个 CID 的各个部分。 

| CID | UUID | 命令代码 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_MODEM_LOGGING_CONFIG | UUID_BASIC_CONNECT_EXTENSIONS | TBD | Y | Y | Y |

## <a name="mbim_cid_modem_logging_config"></a>MBIM_CID_MODEM_LOGGING_CONFIG

此 CID 用于配置调制解调器收集的日志和通过 DSS 从调制解调器发送到主机的频率。 在启动日志记录会话之前，必须配置日志记录。 由于此 CID 是连接扩展的一部分，因此它对于 Ihv 支持此 CID 是可选的。 如果 IHV 通过 DSS 数据通道支持调制解调器日志记录，则必须将其指定为功能。 可使用 MBIM_BASIC_CID_DEVICE_SERVICES CID 播发此功能。

### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MODEM_LOGGING_CONFIG | 不适用 | 不适用 |
| 响应 | MBIM_MODEM_LOGGING_CONFIG | MBIM_MODEM_LOGGING_CONFIG | MBIM_MODEM_LOGGING_CONFIG |

### <a name="query"></a>查询

查询当前的调制解调器日志记录配置。 不使用 MBIM_COMMAND_MSG 的 InformationBuffer。 以下 MBIM_MODEM_LOGGING_CONFIG 结构在 MBIM_COMMAND_DONE 的 InformationBuffer 中使用。

#### <a name="mbim_modem_logging_config"></a>MBIM_MODEM_LOGGING_CONFIG

| Offset | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 版本 | UINT32 | 此结构的版本号。 对于此结构的版本1，此字段必须设置为 **1** 。 |
| 4 | 4 | MaxSegmentSize | UINT32 | 指定调制解调器发送的每个段的段大小（kb）。 如果设备服务的调制解调器支持的最大片段大小超过了设置的值，则此值将设置为支持的最大段大小。 |
| 8 | 4 | MaxFlushTime | UINT32 | 时间（以毫秒为单位），它指示在发送日志片段之前调制解调器等待的最长时间。 如果从上次发送日志片段起，收集的日志在 **MaxFlushTime** 持续时间内不会达到 **MaxSegmentSize** ，则会发送日志片段，而不考虑其大小。 如果没有日志记录数据，则不发送任何通知。 如果设备无法处理更短的刷新时间，则设备将返回它可以在响应中处理的时间。 对查询或集的响应包含当前配置的 **MaxFlushTime**。 |
| 12 | 4 | LevelConfig | MBIM_LOGGING_LEVEL_CONFIG | 配置为其收集日志的级别。 对查询或集的响应包含当前配置的 **LevelConfig**。 |

> [!NOTE]
> 如果调制解调器无法在请求的 **MaxSegmentSize** 和 **MAXFLUSHTIMER** 上向操作系统提供日志数据，则可以为这些参数选择其自己的值，并将 OS 更新为设置响应或未经请求的事件。 当 **MaxSegmentSize** 或 **MaxFlushTimer** 更改时，操作系统行为不会更改，因为它会接收数据包，而不考虑将它们转储到文件的情况。

以下 MBIM_LOGGING_LEVEL_CONFIG 枚举用于前面的 MBIM_MODEM_LOGGING_CONFIG 结构。

| 类型 | 值 | 描述 |
| --- | --- | --- |
| MBIMLoggingLevelProd | 0 | 用于从零售或生产填充收集遥测数据。 生成的日志应该是胶囊大小的，并且仅包含关键调制解调器或 MBB 状态或故障信息。 |
| MBIMLoggingLevelLabVerbose | 1 | 用于开发低成熟度的 MBB 产品。 对调制解调器进行详细的完整堆栈捕获。 生成的调制解调器捕获应允许 IHV 重播并在日志中完全恢复捕获。 |
| MBIMLoggingLevelLabMedium | 2 | 适用于 MBB 产品的验证和现场测试，具有相对成熟度和稳定性。 详细程度和详细程度为 IHV 工程师提供了足够的数据点，可用于诊断最 MBB 的故障。 |
| MBIMLoggingLevelLabLow | 3 | 适用于自行主机级别的日志记录。 完整堆栈捕获调制解调器的摘要级别捕获。 启用对调制解调器状态和操作系统交互的突出显示。 |
| MBIMLoggingLevelOem | 4 | 保留以供 OEM 和 IHV 内部使用。 |

### <a name="set"></a>设置

Set 命令用于设置以配置调制解调器日志记录的级别、段大小和最大刷新时间。 MBIM_MODEM_LOGGING_CONFIG 结构在 InformationBuffer 中使用。

### <a name="response"></a>响应

MBIM_COMMAND_DONE 中的 InformationBuffer 包含 MBIM_MODEM_LOGGING_CONFIG 的结构。

### <a name="unsolicited-events"></a>未经请求的事件

在调制解调器需要通知操作系统有关内部更改的情况下，支持未经请求的事件。 目前，Windows 10 版本1903中不会出现这些情况。

### <a name="status-codes"></a>状态代码

此 CID 仅使用 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的9.4.5 部分中定义的通用状态代码。

## <a name="dss-session-behavior-during-inactivity"></a>不活动期间的 DSS 会话行为

下表描述了 DSS 会话在各个非活动阶段的行为方式：

| 方案 | DSS 会话状态 |
| --- | --- |
| 系统睡眠，仅调制解调器睡眠、重置和恢复 | DSS 会话保持打开状态 |
| 系统关闭、重新启动、休眠 | DSS 会话已关闭 |
