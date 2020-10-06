---
title: MB 低级别 UICC 访问
description: MB 低级别 UICC 访问
ms.assetid: AD0E9F20-9C95-4102-94EF-054D45E2C597
keywords:
- MB 低级别 UICC 访问，移动宽带低级别 UICC 访问，移动宽带微型端口驱动程序低级 UICC，MB UICC ATR，MB UICC 重置答案，MB UICC 打开通道，MB UICC 关闭通道，MB UICC APDU，MB UICC 终端功能，MB UICC 重置
ms.date: 12/05/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7b15c31f1c910233c62b4dd96cf1ebaff473a428
ms.sourcegitcommit: 20eac54e419a594f7cea766ee28f158559dfd79c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91754963"
---
# <a name="mb-low-level-uicc-access"></a>MB 低级别 UICC 访问

## <a name="overview"></a>概述

移动宽带接口型号版本1.0 或 MBIM1 定义了主机设备与蜂窝数据调制解调器之间的 OEM 和 IHV 无关的接口。

MBIM1 函数包括 UICC 智能卡，并提供对其某些数据和内部状态的访问。 不过，智能卡可能包含了 MBIM 接口定义以外的其他功能。 这些附加功能包括支持基于近现场通信的移动支付解决方案的安全元素，或用于整个 UICC 配置文件的远程设置。

在启用移动宽带的 Windows 设备中，除了 (RIL) 接口的无线电接口层，还使用了 MBIM 接口。 RIL 提供的功能之一是用于访问 UICC 的低级别访问的接口。 本主题介绍 MBIM 中的一组 Microsoft 扩展，这些扩展介绍了 MBIM 接口上的此附加功能。

Microsoft 扩展包含一组设备服务命令 (集和查询) 和通知。 这些扩展不包括设备服务流的任何新使用。

## <a name="mbim-service-and-cid-values"></a>MBIM 服务和 CID 值

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft 低级别 UICC 访问 | UUID_MS_UICC_LOW_LEVEL | C2F6588E-F037-4BC9-8665-F4D44BD09367 |

下表指定了每个 CID 的命令代码，以及 CID 是否支持 Set、Query 或 Event (通知) 请求。 有关其参数、数据结构和通知的详细信息，请参阅本主题中的每个 CID 的各个部分。 

| CID | 命令代码 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- | --- |
| MBIM_CID_MS_UICC_ATR | 1 | N | Y | N |
| MBIM_CID_MS_UICC_OPEN_CHANNEL | 2 | Y | N | N |
| MBIM_CID_MS_UICC_CLOSE_CHANNEL | 3 | Y | N | N |
| MBIM_CID_MS_UICC_APDU)  | 4 | Y | N | N |
| MBIM_CID_MS_UICC_TERMINAL_CAPABILITY | 5 | Y | Y | N |
| MBIM_CID_MS_UICC_RESET | 6 | Y | Y | N |

## <a name="status-codes"></a>状态代码

MBIM 状态代码在 [MBIM 标准](https://www.usb.org/document-library/mobile-broadband-interface-model-v10-errata-1-and-adopters-agreement)的9.4.5 节中定义。 此外，还定义了下列附加的失败状态代码：

| 状态代码 | 值 (hex)  | 说明 |
| --- | --- | --- |
| MBIM_STATUS_MS_NO_LOGICAL_CHANNELS | 87430001 | 逻辑通道打开失败，因为 UICC 上没有可用的逻辑通道， (该通道不支持这些逻辑通道，或者所有逻辑通道均) 使用。 |
| MBIM_STATUS_MS_SELECT_FAILED | 87430002 | 由于选择失败，逻辑通道打开失败。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 87430003 | 逻辑频道号无效 (未 MBIM_CID_MS_UICC_OPEN_CHANNEL) 打开它。 |

### <a name="mbim_subscriber_ready_state"></a>MBIM_SUBSCRIBER_READY_STATE

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MBIMSubscriberReadyStateNoEsimProfile | 7 | 该卡已准备就绪，但没有任何已启用的配置文件。 |

## <a name="uicc-responses-and-status"></a>UICC 响应和状态

UICC 可以实现基于字符或基于记录的接口，也可以同时实现两者。 尽管特定机制有所不同，但结果是 UICC 响应每个具有两个状态字节 (名为 SW1 和 SW2) 的命令以及可能为空) 的响应 (。 正常成功状态由 90 00 指示。 但是，如果 UICC 支持卡应用程序工具包，并且 UICC 希望向终端发送一个主动命令，则成功的返回将由 91 XX (状态指示，其中 XX 发生变化) 。 MBIM 函数（或终端）负责处理此主动命令，就像它处理在任何其他 UICC 操作期间接收到的主动命令一样 (将提取发送到 UICC，处理主动命令，或将其发送到具有 MBIM_CID_STK_PAC) 的主机。 当 MBIM 主机发送 MBIM_CID_MS_UICC_OPEN_CHANNEL 或 MBIM_CID_MS_UICC_APDU 时，应将 90 00 和 91 XX 视为正常状态。

命令必须能够返回大于256字节的响应。 此机制在 [ISO/IEC 7816-4:2013 标准](https://go.microsoft.com/fwlink/p/?linkid=864596)的5.1.3 部分中进行了介绍。 在这种情况下，该卡将返回 61 XX 的 SW1 SW2 状态字，而不是 90 00，其中 XX 是剩余字节数或00（如果有256字节或更多剩余）。 必须重复使用相同的类字节发出 GET 响应，直到接收到所有数据为止。 最终状态字词为 90 00。 序列必须在特定的逻辑通道内不间断。 其他 Apdu 应在调制解调器上处理，并且应对主机是透明的。 如果在主机中进行了处理，则不能保证在 Apdu 序列中，某些其他 APDU 可能会以异步方式引用卡。

## <a name="comparison-to-ihvril"></a>与 IHVRIL 的比较

IHVRIL 规范的5.2.3.3.10 到5.2.3.3.14 部分定义了此规范所基于的类似接口。 一些差异包括：

- RIL 接口不提供指定安全消息传送的方法。 MBIM 命令到 exchange Apdu 将此参数指定为显式参数。
- RIL 接口不清楚地定义 APDU 内类字节的解释。 MBIM 规范规定，从主机发送的类字节必须存在，但不 (使用，而 MBIM 函数则会) 构造此字节。
- RIL 接口使用单独的函数关闭组中的所有 UICC 通道，而 MBIM 接口使用单个 CID 的变量参数实现此功能。
- 与 RIL 错误和 UICC 状态之间的关系相比，MBIM 错误状态和 UICC 状态 (SW1 SW2) 之间的关系更清晰地定义。
- MBIM 接口将无法从失败分配新的逻辑通道以选择指定的应用程序。
- MBIM 接口允许发送要发送到卡的调制解调器终端功能对象。

## <a name="mbim_cid_ms_uicc_atr"></a>MBIM_CID_MS_UICC_ATR

重置 (ATR) 的答案是执行重置后 UICC 发送的第一个字符串。 它描述了卡的功能，如它支持的逻辑通道数。 MBIM 函数在从 UICC 接收到 ATR 时必须保存它。 随后，主机可以使用 MBIM_CID_MS_UICC_ATR 命令来检索 ATR。

### <a name="parameters"></a>参数

|  类型 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | 空 | 不适用 |
| 响应 | 不适用 | MBIM_MS_ATR_INFO | 不适用 |

### <a name="query"></a>查询

查询消息的 InformationBuffer 为空。 

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

MBIM_COMMAND_DONE 的 InformationBuffer 包含以下 MBIM_MS_ATR_INFO 结构，该结构描述为附加到此函数的 UICC 重置的答案。

#### <a name="mbim_ms_atr_info"></a>MBIM_MS_ATR_INFO

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AtrSize | 大小 (0 ... 33)  | **AtrData**的长度。 |
| 4 | 4 | AtrOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个名为 **AtrData** 的字节数组，其中包含 ATR 数据。 |
| 8 | AtrSize | DataBuffer | DATABUFFER | **AtrData**字节数组。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

以下状态代码适用。

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |

## <a name="mbim_cid_ms_uicc_open_channel"></a>MBIM_CID_MS_UICC_OPEN_CHANNEL

主机使用 MBIM_CID_MS_UICC_OPEN_CHANNEL 命令请求函数在 UICC 卡上打开一个新的逻辑通道，并选择由其应用程序 ID) 指定的指定 UICC 应用程序 (。

函数使用 UICC 命令序列实现此 MBIM 命令：

1.  函数向 UICC 发送管理通道命令，如 [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的第11.1.17 节所述，创建新的逻辑通道。 如果此命令失败，则该函数返回 SW1 SW2 的 MBIM_STATUS_MS_NO_LOGICAL_CHANNELS 状态，而不执行进一步的操作。 
2.  如果 "管理通道" 命令成功，则 UICC 报告该函数的新逻辑通道的通道号。 函数按 [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的节11.1.1 中所述发送 P1 = 04 的 SELECT [by name] 命令。 如果此操作失败，则此函数会将 "管理通道" 命令发送到 UICC，以关闭逻辑通道，并通过 SELECT 返回 SW1 SW2 的 MBIM_STATUS_MS_SELECT_FAILED 状态。
3.  如果 SELECT 命令成功，则该函数将记录由主机指定的逻辑通道号和通道组，以供将来参考。 然后，它将从 SELECT 返回逻辑通道号，SW1 SW2，并将响应从 SELECT 返回到主机。

### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_SET_UICC_OPEN_CHANNEL | 不适用 | 不适用 |
| 响应 | MBIM_MS_UICC_OPEN_CHANNEL_INFO | 不适用 | 不适用 |

### <a name="query"></a>查询

不适用。

### <a name="set"></a>设置

MBIM_COMMAND_MSG 的 InformationBuffer 包含以下 MBIM_MS_SET_UICC_OPEN_CHANNEL 结构。

#### <a name="mbim_ms_set_uicc_open_channel"></a>MBIM_MS_SET_UICC_OPEN_CHANNEL

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AppIdSize | 大小 (0 .0)  | 应用程序 ID (AppId) 的大小。 |
| 4 | 4 | AppIdOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个名为 **appid** 的字节数组，用于定义要选择的 appid。 |
| 8 | 4 | SelectP2Arg | UINT32 (0 .0)  | 选择命令的 *P2* 参数。 |
| 12 | 4 | ChannelGroup | UINT32 | 标识此通道的通道组的标记值。 |
| 16 | AppIdSize | DataBuffer | DATABUFFER | **AppId**字节数组。 |

### <a name="response"></a>响应

MBIM_COMMAND_DONE 的 InformationBuffer 包含以下 MBIM_MS_UICC_OPEN_CHANNEL_INFO 结构。

#### <a name="mbim_ms_uicc_open_channel_info"></a>MBIM_MS_UICC_OPEN_CHANNEL_INFO

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状态 | BYTE [2] | SW1 和 SW2，以字节顺序排列。 有关详细信息，请参阅此表后面的说明。 |
| 4 | 4 | 通道 | UINT32 (0. 19)  | 逻辑通道标识符。 如果此成员是0，则操作失败。 |
| 8 | 4 | ResponseLength | 大小 (0 .0)  | 响应长度（以字节为单位）。 |
| 12 | 4 | ResponseOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个名为 **response** 的字节数组，其中包含来自 SELECT 的响应。 |
| 16 | - | DataBuffer | DATABUFFER | **响应**字节数组数据。 |

如果命令返回 MBIM_STATUS_MS_NO_LOGICAL_CHANNELS，则 " **状态** " 字段应包含 "管理通道" 命令中的 "UICC 状态字词 SW1" 和 "SW2"，其余字段将为零。 如果命令返回 MBIM_STATUS_MS_SELECT_FAILED，则 " **状态** " 字段应包含 "SELECT" 命令中的 "UICC 状态 SW1" 和 "SW2"，其余字段将为零。 对于任何其他状态，InformationBuffer 应为空。

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

以下状态代码适用：

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |
| MBIM_STATUS_MS_NO_LOGICAL_CHANNELS | 逻辑通道打开失败，因为 UICC 上没有可用的逻辑通道， (该通道不支持它们，或者所有它们都) 使用。 |
| MBIM_STATUS_MS_SELECT_FAILED | 由于选择失败，逻辑通道打开失败。 |

## <a name="mbim_cid_ms_uicc_close_channel"></a>MBIM_CID_MS_UICC_CLOSE_CHANNEL

主机将 MBIM_CID_MS_UICC_CLOSE_CHANNEL 发送到函数以关闭 UICC 上的逻辑通道。 主机可以指定频道号，也可以指定通道组。

如果主机指定了通道号，则该函数应检查该通道是否已由上一个 MBIM_CID_MS_UICC_OPEN_CHANNEL 打开。 如果是这样，则应将 "管理通道" 命令发送到 UICC 以关闭通道，返回 MBIM_STATUS_SUCCESS 状态，并从管理通道返回 SW1 SW2。 如果不是，则应不执行任何操作并返回 MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL 故障状态。

如果主机指定了一个通道组，则该函数将确定哪个 (如果任何) 的逻辑通道使用该通道组打开，并向每个此类通道的 UICC 发送一个 "管理通道" 命令。 它将返回 MBIM_STATUS_SUCCESS 状态 SW1，其中包含上一个管理通道的 SW2。 如果通道未关闭，则它应返回 90 00。

### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_SET_UICC_CLOSE_CHANNEL | 不适用 | 不适用 |
| 响应 | MBIM_MS_UICC_CLOSE_CHANNEL_INFO | 不适用 | 不适用 |

### <a name="query"></a>查询

不适用。

### <a name="set"></a>设置

MBIM_COMMAND_MSG 的 InformationBuffer 包含以下 MBIM_MS_SET_UICC_CLOSE_CHANNEL 结构。

#### <a name="mbim_ms_set_uicc_close_channel"></a>MBIM_MS_SET_UICC_CLOSE_CHANNEL

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 通道 | UINT32 (0. 19)  | 如果为非零，则指定要关闭的通道。 如果为零，则指定与 **ChannelGroup** 关联的信道 (s) 将关闭。 |
| 4 | 4 | ChannelGroup | UINT32 | 如果 **通道** 为零，此值将指定一个标记值，并关闭带有此标记的所有通道。 如果 **通道** 为非零，则忽略此字段。

### <a name="response"></a>响应

MBIM_COMMAND_DONE 的 InformationBuffer 包含以下 MBIM_MS_UICC_CLOSE_CHANNEL_INFO 结构。

#### <a name="mbim_ms_uicc_close_channel_info"></a>MBIM_MS_UICC_CLOSE_CHANNEL_INFO

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状态 | BYTE [2] | 由函数代表此命令执行的最后一个管理通道的 SW1 和 SW2。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 逻辑信道号无效 (换言之，它不是用 MBIM_CID_MS_UICC_OPEN_CHANNEL) 打开的。 |

## <a name="mbim_cid_ms_uicc_apdu"></a>MBIM_CID_MS_UICC_APDU

主机使用 MBIM_CID_MS_UICC_APDU 将命令 APDU 发送到 UICC 上的指定逻辑通道，并接收响应。 MBIM 函数应确保该逻辑通道以前是用 MBIM_CID_MS_UICC_OPEN_CHANNEL 打开的，如果不是，则会失败，状态为 MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL。

主机必须向函数发送一个完全 APDU。 可以使用 [ISO/IEC 7816-4:2013 标准](https://go.microsoft.com/fwlink/p/?linkid=864596)的第4部分中的第一个 interindustry 定义中定义的一个类字节值，也可以在 [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的部分10.1.1 的扩展定义中发送 APDU。 可以在没有安全消息传送的情况下发送 APDU，也可以通过安全消息传送。 未验证命令头。 主机指定类字节、逻辑通道号和安全消息传送的类型以及 APDU。

Command APDU 的第一个字节是类 byte，编码为由 [ISO/IEC 7816-4:2013 标准](https://go.microsoft.com/fwlink/p/?linkid=864596) 或 [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的节10.1.1 的第4部分定义。 主机可以发送0X、4X、6倍、8X、CX 或 EX 类字节。 但是，此函数不会将此字节直接传递到 UICC。 相反，在将 APDU 发送到 UICC 之前，该函数会将主机中的第一个字节替换为新的类字节， (按照由主机指定的类型、通道和 SecureMessaging 值的[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)) 的第[7816-4:2013](https://go.microsoft.com/fwlink/p/?linkid=864596) 4 部分的规定进行编码：

| Byte 类 | 说明 |
| --- | --- |
| 0X | 7816-4 interindustry，1 <= 通道 <= 3，则编码低位字节的安全性（如果相关） |
| 4X | 7816-4 interindustry，4 <= 通道 <= 19，无安全消息 |
| 6倍 | 7816-4 interindustry，4 <= 通道 <= 19，安全 (标头未进行身份验证)  |
| .8X | 102 221 扩展，1<= 通道 <= 3，则编码低位字节的安全性（如果相关） |
| CX | 102 221 扩展，4 <= 通道 <= 19，无安全消息传送 |
| EX | 102 221 扩展，4 <= 通道 <= 19，安全 (标头未进行身份验证)  |

函数应返回状态 SW1 SW2 和从 UICC 到主机的响应。

### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_SET_UICC_APDU | 不适用 | 不适用 |
| 响应 | MBIM_MS_UICC_APDU_INFO | 不适用 | 不适用 |

### <a name="query"></a>查询

不适用。

### <a name="set"></a>设置

MBIM_COMMAND_MSG 的 InformationBuffer 包含以下 MBIM_MS_SET_UICC_APDU 结构。

#### <a name="mbim_ms_set_uicc_apdu"></a>MBIM_MS_SET_UICC_APDU

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 通道 | UINT32 (1. 19)  | 指定要将 APDU 发送到的通道。 |
| 4 | 4 | SecureMessaging | MBIM_MS_UICC_SECURE_MESSAGING | 指定是否使用安全消息交换 APDU。 |
| 8 | 4 | 类型 | MBIM_MS_UICC_CLASS_BYTE_TYPE | 指定类字节定义的类型。 |
| 12 | 4 | CommandSize | UINT32 (261)  | **命令**长度（字节）。 |
| 16 | 4 | CommandOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量为一个名为的 **命令** ，该数组包含 APDU。 |
| 20 | - | DataBuffer | DATABUFFER | **命令**字节数组。 |

MBIM_MS_SET_UICC_APDU 结构使用以下 MBIM_MS_UICC_SECURE_MESSAGING 和 MBIM_MS_UICC_CLASS_BYTE_TYPE 的数据结构。

##### <a name="mbim_ms_uicc_secure_messaging"></a>MBIM_MS_UICC_SECURE_MESSAGING

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MBIMMsUiccSecureMessagingNone | 0 | 无安全消息。 |
| MBIMMsUiccSecureMessagingNoHdrAuth | 1 | 安全消息传送，未对命令头进行身份验证。 |

##### <a name="mbim_ms_uicc_class_byte_type"></a>MBIM_MS_UICC_CLASS_BYTE_TYPE

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MBIMMsUiccInterindustry | 0 | 根据 ISO 7816-4 中的第一个 interindustry 定义定义。 |
| MBIMMsUiccExtended | 1 | 根据 ETSI 102 221 中的扩展定义定义。 |

### <a name="response"></a>响应

MBIM_COMMAND_DONE 的 InformationBuffer 包含以下 MBIM_MS_UICC_APDU_INFO 结构。

#### <a name="mbim_ms_uicc_apdu_info"></a>MBIM_MS_UICC_APDU_INFO

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状态 | BYTE [2] | 命令生成的 SW1 和 SW2 状态字词。 |
| 4 | 4 | ResponseLength | SIZE | 响应长度（以字节为单位）。 |
| 8 | 4 | ResponseOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个名为 **response** 的字节数组，其中包含来自 SELECT 的响应。 |
| 12 | - | DataBuffer | DATABUFFER | **响应**字节数组。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

以下状态代码适用：

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 逻辑信道号无效 (换言之，它不是用 MBIM_CID_MS_UICC_OPEN_CHANNEL) 打开的。 |

如果该函数可以将 APDU 发送到 UICC，则它将返回 MBIM_STATUS_SUCCESS 以及 SW1 SW2 状态字和来自 UICC 的响应 (如果任何) 。 宿主必须检查状态 (SW1 SW2) ，以确定是否在 UICC 上成功或失败的原因。

## <a name="mbim_cid_ms_uicc_terminal_capability"></a>MBIM_CID_MS_UICC_TERMINAL_CAPABILITY

主机发送 MBIM_CID_MS_UICC_TERMINAL_CAPABILITY 来通知调制解调器主机的功能。 在选择第一个应用程序之前，必须将 " [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)" 的 "11.1.19" 部分中指定的终端功能 APDU 发送到卡， (如果该应用程序) 支持。 因此，主机不能直接发送终端功能 APDU，而是发送 MBIM_CID_MS_UICC_TERMINAL_CAPABILITY 命令，该命令包含一个或多个将永久存储在调制解调器上的终端功能对象。 在下一个卡插入或重置时，在 ATR 后，调制解调器会选择 MF 并检查是否支持终端功能。 如果是这样，则调制解调器将与 MBIM_CID_MS_UICC_TERMINAL_CAPABILITY 命令指定的信息以及任何调制解调器生成的信息一起发送终端功能 APDU。

### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_SET_UICC_TERMINAL_CAPABILITY | 空 | 不适用 |
| 响应 | 不适用 | MBIM_MS_TERMINAL_CAPABILITY_INFO | 不适用 |

### <a name="query"></a>查询

InformationBuffer 应为 null，而 InformationBufferLength 应为零。

### <a name="set"></a>设置

MBIM_COMMAND_MSG 的 InformationBuffer 包含以下 MBIM_MS_SET_UICC_TERMINAL_CAPABILITY 结构。

#### <a name="mbim_ms_set_uicc_terminal_capability"></a>MBIM_MS_SET_UICC_TERMINAL_CAPABILITY

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 | UINT32 | 终端功能对象的元素计数。 |
| 4 | 8 * EC | CapabilityList OL_PAIR_LIST| 每个终端功能对象 TLV 的偏移长度对列表。 |
| 4 + 8 * EC | - | DataBuffer | DATABUFFER | 实际终端功能对象 TLVs 的字节数组。 |

### <a name="response"></a>响应

响应将包含与上次发送的终端功能对象连接到调制解调器的完全相同的 SET 命令。 因此，MBIM_MS_TERMINAL_CAPABILITY_INFO 与 MBIM_MS_SET_UICC_TERMINAL_CAPABILITY 相同。

#### <a name="mbim_ms_terminal_capability_info"></a>MBIM_MS_TERMINAL_CAPABILITY_INFO

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 | UINT32 | 终端功能对象的元素计数。 |
| 4 | 8 * EC | CapabilityList OL_PAIR_LIST| 每个终端功能对象 TLV 的偏移长度对列表。 |
| 4 + 8 * EC | - | DataBuffer | DATABUFFER | 实际终端功能对象 TLVs 的字节数组。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 逻辑信道号无效 (换言之，它不是用 MBIM_CID_MS_UICC_OPEN_CHANNEL) 打开的。 |

## <a name="mbim_cid_ms_uicc_reset"></a>MBIM_CID_MS_UICC_RESET

主机将 MBIM_CID_MS_UICC_RESET 发送到 MBIM 函数，以重置 UICC 或查询函数的传递状态。

当宿主请求函数重置 UICC 时，它将指定一个传递操作。

如果主机指定了 *MBIMMsUICCPassThroughEnable* passthrough 操作，则该函数将重置 UICC，并在 UICC 开启后将该 UICC 视为模式，该模式允许主机和 (UICC 之间进行通信，即使 UICC 没有电信 UICC 文件系统) 。 此函数不会将任何 Apdu 发送到卡，并且不会在主机与 UICC 之间的通信的任何时候干扰。

如果主机指定了 *MBIMMsUICCPassThroughDisable* passthrough 操作，则该函数将重置 UICC，并在 UICC 开启后将该 UICC 视为常规电信 UICC，并期望在 UICC 上存在一个电信 UICC 文件系统。

当主机查询函数来确定 passthrough 状态时，如果函数以 *MBIMMsUICCPassThroughEnabled* 状态响应，则表示启用了直通模式。 如果函数以 *MBIMMsUICCPassThroughDisabled* 状态进行响应，则表示已禁用直通模式。

### <a name="parameters"></a>参数

| 类型  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_SET_UICC_RESET | 空 | 不适用 |
| 响应 | MBIM_MS_UICC_RESET_INFO | MBIM_MS_UICC_RESET_INFO | 不适用 |

### <a name="query"></a>查询

InformationBuffer 应为 null，而 *InformationBufferLength* 应为零。

### <a name="set"></a>设置

#### <a name="mbim_set_ms_uicc_reset"></a>MBIM_SET_MS_UICC_RESET

MBIM_SET_MS_UICC_RESET 结构包含由主机指定的通过操作。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PassThroughAction | MBIM_MS_UICC_PASSTHROUGH_ACTION | 有关详细信息，请参阅 [MBIM_MS_UICC_PASSTHROUGH_ACTION](#mbim_ms_uicc_passthrough_action)。 |

#### <a name=""></a><a name="mbim_ms_uicc_passthrough_action">MBIM_MS_UICC_PASSTHROUGH_ACTION</a>

MBIM_MS_UICC_PASSTHROUGH_ACTION 枚举定义宿主可以指定给 MBIM 函数的传递操作的类型。

| 类型 | 值 |
| --- | --- |
| MBIMMsUiccPassThroughDisable | 0 |
| MBIMMsUiccPassThroughEnable | 1 |

### <a name="response"></a>响应

#### <a name="mbim_ms_uicc_reset_info"></a>MBIM_MS_UICC_RESET_INFO

MBIM_MS_UICC_RESET_INFO 结构包含 MBIM 函数的传递状态。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PassThroughStatus | MBIM_MS_UICC_PASSTHROUGH_STATUS | 有关详细信息，请参阅 [MBIM_MS_UICC_PASSTHROUGH_STATUS](#mbim_ms_uicc_passthrough_status)。 |

#### <a name=""></a><a name="mbim_ms_uicc_passthrough_status">MBIM_MS_UICC_PASSTHROUGH_STATUS</a> 

MBIM_MS_UICC_PASSTHROUGH_STATUS 枚举定义 MBIM 函数指定给主机的传递状态的类型。

| 类型 | 值 |
| --- | --- |
| MBIMMsUiccPassThroughDisabled | 0 |
| MBIMMsUiccPassThroughEnabled | 1 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_BUSY | 设备处于繁忙状态。 |
| MBIM_STATUS_FAILURE | 此操作失败。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 设备不支持此操作。 |

### <a name="oid_wwan_uicc_reset"></a>OID_WWAN_UICC_RESET

[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)MBIM_CID_MS_UICC_RESET 的 NDIS 等效项。 


