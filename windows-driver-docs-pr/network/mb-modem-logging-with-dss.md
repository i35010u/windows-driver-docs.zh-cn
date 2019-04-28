---
title: 使用 DSS 进行 MB 调制解调器日志记录
description: 使用 DSS 进行 MB 调制解调器日志记录
ms.assetid: A40EAF7C-A808-4C2D-848C-EAD2D639EB55
keywords:
- 使用 DSS，移动宽带调制解调器使用 DSS 进行日志记录的 MB 调制解调器日志记录
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d9f4869fed3c1929f35520eccc6811d7d24ed7e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343304"
---
# <a name="mb-modem-logging-with-dss"></a>使用 DSS 进行 MB 调制解调器日志记录

## <a name="overview"></a>概述

本主题介绍新的标准 Windows 移动宽带 (MBB) 日志记录接口通过 USB MBIM 1.0 规范，在 Windows 10，版本 1903年及更高版本中提供的 Microsoft 扩展。 

与此新的日志记录接口，操作系统可以通知 MBB 设备启动、 停止，并将日志刷新到操作系统文件系统通过 MBIM CID 命令。 考虑到的调制解调器的日志记录有效负载，MBB 服务使用传输到 OS 使用 MBB 数据服务 Stream (DSS) 的日志记录有效负载的数据通道的非 IP 特性。 在中定义 DSS[移动宽带接口模型 (MBIM) 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)规范。 

操作系统抽象化跨整个 MBB 生态系统使用一组特定于 Windows 的 MBB 日志记录配置调制解调器的诊断功能和配置。 这些 MBB 日志记录配置启用调制解调器供应商联系，以将 OS MBB 日志记录要求映射到相应的内部日志记录配置。 提取和由操作系统定义的日志记录配置包括 MBB 日志记录详细程度级别和最大刷新时间。 

调制解调器使填充其日志记录缓冲区，直到达到最大缓冲区的大小，直到填充段和 MBIM framework 将传输到 OS 中，段或它的最大的刷新时间达到 （即使未填充段） 时刷新其缓冲区的内容。 OS 定义日志记录配置级别，本主题后面所述的标准 Windows MBB 一的组。 每个配置级别指定 MBB 日志记录详细信息和详细级别操作系统的抽象。

MBB 配置级别操作系统抽象映射到相应的内置调制解调器配置调制解调器。 操作系统不提供任何其他配置的负载，例如日志记录筛选器或掩码，到非 OS MBB 配置级别的调制解调器。 

有关支持日志记录的 MBB 的调制解调器，所有日志记录配置级别除了 MBIMLoggingLevelOem 的 MBB 上必须存在所有 BSP 变体。 换而言之，IHV 或 OEM 必须支持 PROD 或实验室级别的 MBB 生产和研发 BSP 版本中的日志记录。 仅可以从操作系统禁用实验室 MBB 日志记录级别。

此新的日志记录接口设计使用控制通道来设置日志记录参数，并使用的数据通道收到调制解调器日志，因为数据通道专门用于将数据大容量调制解调器。 这种设计的优点是不需要通过控制通道，从而使设备性能保持一致传输数据的大容量。 它还会于更高的吞吐量。 数据通道运营的 DSS 命令。 对于调制解调器示例流可能如下所示：

1. 操作系统发送到调制解调器，若要配置日志记录参数，如 MaxSegmentSize、 MaxFlushTime 和 LoggingLevel MBIM_CID_MODEM_LOGGING_CONFIG CID。
2. 一旦 OS 从调制解调器收到成功响应后，会将 MBIM_CID_DSS_CONNECT DSS 命令发送到调制解调器的具有特定 GUID 的调制解调器日志记录、 MBIMDssLinkActivate 状态和唯一的 DSS 会话 id。
3. 一旦收到成功状态代码，OS 准备接收从调制解调器的片段。 这些片断称为 DataServiceSessionRead 数据包。
4. DataServiceSessionRead 数据包继续到达直到操作系统发出另一个 MBIM_CID_DSS_CONNECT 命令，使用相同的 DSS 会话 ID 和 MBIMDSSLinkDeactivate 状态。

## <a name="modem-logging-data-path"></a>调制解调器日志记录数据路径

Moddem 日志记录使用 MBIM 数据服务 Stream (DSS) 传输的日志记录有效负载数据。 DSS 有关的详细信息，请参阅部分 10.5.38 [MBIM 1.0 规范](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。 

当连接或断开与 DSS 时，下列 GUID 用于调制解调器日志记录：

| GUID | ReplTest1 |
| --- | --- |
| ModemFileTransfer GUID | 0EBB1CEB-AF2D-484D-8DF3-53BC51FD162C |

以下流程图说明了 DSS 安装和卸载过程。

![DSS 调制解调器日志记录设置和关闭流关系图](images/mb-modem-logging-dss-flow.png "DSS 调制解调器日志记录设置和关闭流关系图。")

## <a name="ndis-interface-extension"></a>NDIS 接口扩展

已在 Windows 10，版本 1903，若要支持的调制解调器日志记录中定义了以下 OID。

- [OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)

## <a name="mbim-service-and-cid-values"></a>MBIM 服务和 CID 值

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft Basic IP 连接扩展 | UUID_BASIC_CONNECT_EXTENSIONS | 3d01dcc5-fef5-4d05-9d3a-bef7058e9aaf |

下表指定 UUID 和每个 CID 命令代码，以及是否 CID 支持设置，请查询，或事件 （通知） 请求。 请参阅在本主题中详细了解其参数、 数据结构和通知的每个 CID 的各个部分。 

| CID | UUID | 命令代码 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_MODEM_LOGGING_CONFIG | UUID_BASIC_CONNECT_EXTENSIONS | TBD | Y | Y | Y |

## <a name="mbimcidmodemloggingconfig"></a>MBIM_CID_MODEM_LOGGING_CONFIG

此 CID 用于配置日志收集的调制解调器和何种频率它们将从调制解调器到主机通过发送 DSS。 在启动日志记录会话之前，必须配置日志记录。 由于此 CID 属于连接扩展，对于 Ihv 以支持此 CID 是可选的。 如果 IHV 支持 DSS 数据通道通过调制解调器日志记录，它必须作为一项功能来进行指定。 可以使用 MBIM_BASIC_CID_DEVICE_SERVICES CID 播发功能。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_MODEM_LOGGING_CONFIG | 不适用 | 不适用 |
| 响应 | MBIM_MODEM_LOGGING_CONFIG | MBIM_MODEM_LOGGING_CONFIG | MBIM_MODEM_LOGGING_CONFIG |

### <a name="query"></a>查询

查询当前的调制解调器日志记录配置。 不使用 MBIM_COMMAND_MSG InformationBuffer。 以下 MBIM_MODEM_LOGGING_CONFIG 结构 MBIM_COMMAND_DONE InformationBuffer 中使用。

#### <a name="mbimmodemloggingconfig"></a>MBIM_MODEM_LOGGING_CONFIG

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 此结构的版本号。 此字段必须设置为**1**的版本 1 的此结构。 |
| 4 | 4 | MaxSegmentSize | UINT32 | 指定的段大小，以千字节为单位，每个片段的调制解调器发送。 如果调制解调器设备服务命令支持的最大段大小超出设置的值，则此值设置为受支持的最大段大小。 |
| 8 | 4 | MaxFlushTime | UINT32 | 调制解调器发送日志片段之前，该值指示的最长时间等待的时间，以毫秒为单位。 如果收集的日志不会到达**MaxSegmentSize**内**MaxFlushTime**持续时间，因为最后一个日志片段发送，则日志片段发送而不考虑其大小。 如果没有日志记录的数据，则不发送任何通知。 如果设备不能处理较短的刷新时间，设备对在响应中返回它可以处理的时间。 对查询或一组响应包含当前配置**MaxFlushTime**。 |
| 12 | 4 | LevelConfig | MBIM_LOGGING_LEVEL_CONFIG | 配置会收集日志的级别。 对查询或一组响应包含当前配置**LevelConfig**。 |

> [!NOTE]
> 如果调制解调器不能为在请求 OS 提供的日志数据**MaxSegmentSize**并**MaxFlushTimer**，它可以选择自己的值为这些参数，并更新集响应为操作系统或未经请求的事件。 如果 OS 行为不会更改**MaxSegmentSize**或**MaxFlushTimer**变更，因为它接收的数据包而不考虑，并将它们转储到文件。

上述 MBIM_MODEM_LOGGING_CONFIG 结构中使用以下 MBIM_LOGGING_LEVEL_CONFIG 枚举。

| 在任务栏的搜索框中键入 | 值 | 描述 |
| --- | --- | --- |
| MBIMLoggingLevelProd | 0 | 适用于从零售或生产环境的遥测数据收集。 生成的日志应 capsule 大小且包含密钥的调制解调器或 MBB 状态或失败信息仅。 |
| MBIMLoggingLevelLabVerbose | 1 | 欠成熟与适用于 MBB 产品的开发。 详细完整堆栈捕获的调制解调器。 生成的调制解调器捕获应启用 IHV 重播，并完全恢复日志捕获。 |
| MBIMLoggingLevelLabMedium | 2 | 适用于验证和字段 MBB 产品来测试与相对成熟和稳定。 详细信息和详细程度级别均提供足够的 IHV 工程师来会审大多数 MBB 失败的数据点。 |
| MBIMLoggingLevelLabLow | 3 | 适用于自主机级别日志记录。 完整堆栈捕获调制解调器的摘要级别捕获。 启用突出显示级别了解调制解调器的状态和操作系统交互。 |
| MBIMLoggingLevelOem | 4 | 保留供 OEM 和 IHV 内部使用。 |

### <a name="set"></a>设置

Set 命令用于设置配置级别、 段大小和调制解调器日志记录的最大刷新时间。 MBIM_MODEM_LOGGING_CONFIG 结构 InformationBuffer 中使用。

### <a name="response"></a>响应

在 MBIM_COMMAND_DONE InformationBuffer 包含 MBIM_MODEM_LOGGING_CONFIG 结构。

### <a name="unsolicited-events"></a>未经请求的事件

对于调制解调器需要告知有关内部更改操作系统的方案支持未经请求的事件。 目前，在 Windows 10，版本 1903，这些方案不会发生。

### <a name="status-codes"></a>状态代码

此 CID 仅使用 9.4.5 节中定义的泛型状态代码[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。

## <a name="dss-session-behavior-during-inactivity"></a>DSS 期间处于非活动状态的会话行为

下表描述了 DSS 会话处于非活动状态的各个阶段的行为方式：

| 应用场景 | DSS 会话状态 |
| --- | --- |
| 系统睡眠、 仅限调制解调器的睡眠状态、 重置和恢复 | DSS 会话保持打开状态 |
| 系统关闭、 重新启动、 休眠 | DSS 会话已关闭 |
