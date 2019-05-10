---
title: MB 低级别 UICC 访问
description: MB 低级别 UICC 访问
ms.assetid: AD0E9F20-9C95-4102-94EF-054D45E2C597
keywords:
- MB 低级别 UICC 访问，移动宽带低级别 UICC 访问，移动宽带微型端口驱动程序低级别 UICC、 MB UICC ATR、 MB UICC 应答到重置、 MB UICC 打开通道、 MB UICC 关闭通道，MB UICC APDU MB UICC 终端功能、 MB UICC 重置
ms.date: 12/05/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 335dac6a140dad329d35b83e79080c598e253840
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405222"
---
# <a name="mb-low-level-uicc-access"></a>MB 低级别 UICC 访问

## <a name="overview"></a>概述

移动宽带接口模型修订版本 1.0 或 MBIM1，定义某一主机设备和移动电话网络数据调制解调器之间的 OEM 和 IHV 未知接口。

MBIM1 函数包括 UICC 智能卡，并提供访问某些数据和内部状态。 但是，智能卡可能具有其他功能超越 MBIM 接口定义。 这些附加功能包括对基于近场通信的移动付款解决方案或将整个 UICC 配置文件的远程预配的安全元素的支持。

在移动宽带启用 Windows 设备，除了单选接口层 (RIL) 界面使用 MBIM 接口。 RIL 所提供的功能之一是对 UICC 低级别访问的接口。 本主题介绍一系列 MBIM 描述 MBIM 接口在此附加功能的 Microsoft 扩展。

Microsoft 扩展包含一组设备 （集和查询） 的服务命令和通知。 这些扩展不包含新用途的设备服务流。

## <a name="mbim-service-and-cid-values"></a>MBIM 服务和 CID 值

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft 低级别 UICC 访问 | UUID_MS_UICC_LOW_LEVEL | C2F6588E-F037-4BC9-8665-F4D44BD09367 |

下表为每个 CID，以及是否支持 CID 设置指定的命令代码，查询或事件 （通知） 请求。 请参阅在本主题中详细了解其参数、 数据结构和通知的每个 CID 的各个部分。 

| CID | 命令代码 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- | --- |
| MBIM_CID_MS_UICC_ATR | 1 | N | Y | N |
| MBIM_CID_MS_UICC_OPEN_CHANNEL | 2 | Y | N | N |
| MBIM_CID_MS_UICC_CLOSE_CHANNEL | 3 | Y | N | N |
| MBIM_CID_MS_UICC_APDU) | 4 | Y | N | N |
| MBIM_CID_MS_UICC_TERMINAL_CAPABILITY | 5 | Y | Y | N |
| MBIM_CID_MS_UICC_RESET | 6 | Y | Y | N |

## <a name="status-codes"></a>状态代码

MBIM 状态代码定义中的部分 9.4.5 [MBIM 标准](https://go.microsoft.com/fwlink/p/?linkid=842064)。 此外，定义了以下附加的故障状态代码：

| 状态代码 | 值 （十六进制） | 描述 |
| --- | --- | --- |
| MBIM_STATUS_MS_NO_LOGICAL_CHANNELS | 87430001 | 打开逻辑频道未成功，因为没有逻辑通道位于 UICC （它不支持或所有这些都在使用）。 |
| MBIM_STATUS_MS_SELECT_FAILED | 87430002 | 打开逻辑频道未成功，因为选择失败。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 87430003 | 逻辑频道号无效 （它不通过 MBIM_CID_MS_UICC_OPEN_CHANNEL 打开）。 |

### <a name="mbimsubscriberreadystate"></a>MBIM_SUBSCRIBER_READY_STATE

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMSubscriberReadyStateNoEsimProfile | 7 | 卡已准备但不具有任何已启用配置文件。 |

## <a name="uicc-responses-and-status"></a>UICC 响应和状态

UICC 可实现基于字符的或基于记录的接口中，或两者。 虽然的特定机制不同，但结果是 UICC 响应具有两个状态字节 （名为 SW1 和 SW2） 和响应 （这可能为空） 的每个命令。 正常的成功状态将由 90 00。 但是，如果 UICC 支持卡应用程序工具包和 UICC 想要将主动命令发送到终端，将由 91 XX （其中 XX 而异） 的状态指示成功返回。 MBIM 函数或终端，负责处理此主动命令，就像它会处理任何其他 UICC 操作过程 （将发送一次提取到 UICC、 处理主动命令，或将其发送到主机，MBIM_ 收到主动命令CID_STK_PAC)。 MBIM 主机发送 MBIM_CID_MS_UICC_OPEN_CHANNEL 或 MBIM_CID_MS_UICC_APDU 时应考虑这两个 90 00 和 91 XX 为正常状态。

命令必须能够返回大于 256 个字节的响应。 此机制部分所述 5.1.3 [ISO/IEC 7816-4:2013 标准](https://go.microsoft.com/fwlink/p/?linkid=864596)。 在这种情况下，卡将返回状态字 SW1 SW2 61 XX，而不是 90 00，其中 XX 为剩余的字节数或 00 是否有 256 个字节或剩余的详细信息。 调制解调器必须发出 GET 响应相同的类字节重复之前收到所有数据。 这将由最终状态字 90 00。 序列必须不间断地在特定的逻辑频道中。 其他 Apdu 应在调制解调器处理，并且应该是透明的主机。 如果在主机中处理，则某些其他 APDU Apdu 顺序期间可能会以异步方式引用卡无法保证。

## <a name="comparison-to-ihvril"></a>与 IHVRIL 之间的比较

部分 5.2.3.3.10 通过 5.2.3.3.14 IHVRIL 规范的定义类似此规范所基于的界面。 包括一些差异：

- RIL 接口不提供任何方式来指定安全消息传送。 MBIM 命令来交换 Apdu 指定这作为显式参数。
- RIL 接口不清楚地定义 APDU 中的类字节解释。 必须从主机发送的类字节 MBIM 规范状态存在但未使用 （并改为 MBIM 函数将构造此字节）。
- 该 RIL 界面使用单独的函数来关闭所有 UICC 通道在组中，而 MBIM 接口来实现此目的带有单个 CID 的变体参数。
- MBIM 错误状态和 UICC 状态 (SW1 SW2) 之间的关系是更清楚地定义比 RIL 错误和 UICC 状态之间的关系。
- MBIM 接口用于区分从故障来选择指定的应用程序分配一个新的逻辑通道失败。
- MBIM 接口允许将调制解调器发送要发送到卡的终端的功能对象。

## <a name="mbimcidmsuiccatr"></a>MBIM_CID_MS_UICC_ATR

应答到重置 (ATR) 是执行重置之后，由 UICC 发送的字节数的第一个字符串。 它描述的功能卡，如逻辑它支持的通道数。 MBIM 函数必须保存 ATR 收到从 UICC。 随后，主机可能会使用 MBIM_CID_MS_UICC_ATR 命令检索 ATR。

### <a name="parameters"></a>Parameters

|   | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | 空 | 不适用 |
| 响应 | 不适用 | MBIM_MS_ATR_INFO | 不适用 |

### <a name="query"></a>查询

查询消息的 InformationBuffer 为空。 

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

MBIM_COMMAND_DONE InformationBuffer 包含以下 MBIM_MS_ATR_INFO 结构描述为附加到此函数 UICC 重置的答案。

#### <a name="mbimmsatrinfo"></a>MBIM_MS_ATR_INFO

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AtrSize | SIZE(0..33) | 长度**AtrData**。 |
| 4 | 4 | AtrOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到调用的字节数组**AtrData** ，其中包含 ATR 数据。 |
| 8 | AtrSize | DataBuffer | DATABUFFER | **AtrData**字节数组。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

下面的状态代码都适用。

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |

## <a name="mbimcidmsuiccopenchannel"></a>MBIM_CID_MS_UICC_OPEN_CHANNEL

主机使用 MBIM_CID_MS_UICC_OPEN_CHANNEL 命令请求函数打开一个新的逻辑通道 UICC 卡上，并选择指定的 UICC 应用程序 （由其应用程序 ID 指定）。

函数实现此 MBIM 命令中用一系列 UICC 命令：

1.  该函数将管理通道命令发送到 UICC，如 11.1.17 部分中所述[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)，以创建新的逻辑通道。 如果此命令会失败，该函数返回与 SW1 SW2 MBIM_STATUS_MS_NO_LOGICAL_CHANNELS 状态，并不执行任何进一步的操作。 
2.  如果管理通道命令成功，UICC 函数报告的新逻辑通道的通道数。 该函数将发送 SELECT [名称] 命令其中 P1 = 04 中，如 11.1.1 部分中所述[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 如果此操作失败，该函数将管理通道命令发送到 UICC 关闭逻辑通道，并从 SELECT 返回 SW1 SW2 的 MBIM_STATUS_MS_SELECT_FAILED 状态。
3.  如果选择命令成功，该函数记录逻辑频道号和供将来参考 host 所指定的通道组。 它会返回逻辑频道号、 SW1 SW2 从选择中，并响应从 SELECT 到主机。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_MS_SET_UICC_OPEN_CHANNEL | 不适用 | 不适用 |
| 响应 | MBIM_MS_UICC_OPEN_CHANNEL_INFO | 不适用 | 不适用 |

### <a name="query"></a>查询

不适用。

### <a name="set"></a>设置

MBIM_COMMAND_MSG InformationBuffer 包含以下 MBIM_MS_SET_UICC_OPEN_CHANNEL 结构。

#### <a name="mbimmssetuiccopenchannel"></a>MBIM_MS_SET_UICC_OPEN_CHANNEL

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AppIdSize | SIZE(0..32) | 应用程序 ID (AppId) 的大小。 |
| 4 | 4 | AppIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到调用的字节数组**AppId** ，它定义要选择的 AppId。 |
| 8 | 4 | SelectP2Arg | UINT32(0..255) | *P2* SELECT 命令的参数。 |
| 12 | 4 | ChannelGroup | UINT32 | 标识此通道的通道组的标记值。 |
| 16 | AppIdSize | DataBuffer | DATABUFFER | **AppId**字节数组。 |

### <a name="response"></a>响应

MBIM_COMMAND_DONE InformationBuffer 包含以下 MBIM_MS_UICC_OPEN_CHANNEL_INFO 结构。

#### <a name="mbimmsuiccopenchannelinfo"></a>MBIM_MS_UICC_OPEN_CHANNEL_INFO

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状态 | BYTE[2] | SW1 和 SW2，此字节顺序。 有关详细信息，请参阅此表后面的说明。 |
| 4 | 4 | 通道 | UINT32(0..19) | 逻辑通道标识符。 如果此成员为 0，操作失败。 |
| 8 | 4 | ResponseLength | SIZE(0..256) | 响应长度 （字节）。 |
| 12 | 4 | ResponseOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到调用的字节数组**响应**包含从选择的响应。 |
| 16 | - | DataBuffer | DATABUFFER | **响应**字节数组数据。 |

如果该命令将返回 MBIM_STATUS_MS_NO_LOGICAL_CHANNELS，**状态**字段应包含 UICC 状态中的单词 SW1 和 SW2 管理通道命令，剩余的字段将为零。 如果该命令将返回 MBIM_STATUS_MS_SELECT_FAILED，**状态**字段应包含 UICC 状态中的单词 SW1 和 SW2 SELECT 命令，剩余的字段将为零。 对于任何其他状态，InformationBuffer 应为空。

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

下面的状态代码均适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |
| MBIM_STATUS_MS_NO_LOGICAL_CHANNELS | 打开逻辑通道失败，因为没有逻辑通道位于 UICC （它不支持或所有这些都在使用）。 |
| MBIM_STATUS_MS_SELECT_FAILED | 打开逻辑频道未成功，因为选择失败。 |

## <a name="mbimcidmsuiccclosechannel"></a>MBIM_CID_MS_UICC_CLOSE_CHANNEL

主机将 MBIM_CID_MS_UICC_CLOSE_CHANNEL 发送到函数，以关闭逻辑上 UICC 通道。 主机可以指定频道号，或可以指定通道组。

如果该主机指定频道号，该函数应检查此通道已打开的上一个 MBIM_CID_MS_UICC_OPEN_CHANNEL。 如果是这样，它将向 UICC 以关闭通道，返回的状态为 MBIM_STATUS_SUCCESS，并从管理通道返回 SW1 SW2 发送管理通道命令。 如果不是，它应执行任何操作并返回 MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL 失败状态。

如果该主机指定通道组，此函数将确定其 （如果有） 逻辑通道打开与该通道组并将管理通道命令发送到每个此类通道 UICC。 它返回与最后一个管理通道 SW1 SW2 MBIM_STATUS_SUCCESS 状态。 如果没有通道已关闭，则它应返回 90 00。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_MS_SET_UICC_CLOSE_CHANNEL | 不适用 | 不适用 |
| 响应 | MBIM_MS_UICC_CLOSE_CHANNEL_INFO | 不适用 | 不适用 |

### <a name="query"></a>查询

不适用。

### <a name="set"></a>设置

MBIM_COMMAND_MSG InformationBuffer 包含以下 MBIM_MS_SET_UICC_CLOSE_CHANNEL 结构。

#### <a name="mbimmssetuiccclosechannel"></a>MBIM_MS_SET_UICC_CLOSE_CHANNEL

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 通道 | UINT32(0..19) | 如果非零值，指定要关闭的通道。 如果为零，指定与相关联的频道**ChannelGroup**是要关闭。 |
| 4 | 4 | ChannelGroup | UINT32 | 如果**通道**为零，这将指定的标记值和具有此标记的所有通道已关闭。 如果**通道**为非零值，则忽略此字段。

### <a name="response"></a>响应

MBIM_COMMAND_DONE InformationBuffer 包含以下 MBIM_MS_UICC_CLOSE_CHANNEL_INFO 结构。

#### <a name="mbimmsuiccclosechannelinfo"></a>MBIM_MS_UICC_CLOSE_CHANNEL_INFO

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状态 | BYTE[2] | SW1 和 SW2 由代表此命令的函数执行的最后一个管理通道。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 逻辑频道号不是有效 （即，它不打开与 MBIM_CID_MS_UICC_OPEN_CHANNEL）。 |

## <a name="mbimcidmsuiccapdu"></a>MBIM_CID_MS_UICC_APDU

主机使用 MBIM_CID_MS_UICC_APDU APDU 命令发送到指定的逻辑通道上 UICC 并接收响应。 MBIM 函数应确保使用 MBIM_CID_MS_UICC_OPEN_CHANNEL 以前已经打开逻辑通道，如果它不是状态 MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL 失败。

主机必须将完整 APDU 发送到该函数。 可能使用的第 4 节中的第一个 interindustry 定义中定义的类字节值发送 APDU [ISO/IEC 7816-标准 4:2013](https://go.microsoft.com/fwlink/p/?linkid=864596)，或中的扩展定义中的部分 10.1.1 [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 APDU 可能会发送，但不包含安全消息传送或安全消息传送。 未经过身份验证命令标头。 主机指定的类字节、 逻辑频道号，和安全消息传送以及 APDU 的类型。

该命令的第一个字节 APDU 是编码的第四部分所定义的类字节[ISO/IEC 7816-标准 4:2013](https://go.microsoft.com/fwlink/p/?linkid=864596)符或分节的 10.1.1 [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 主机可能会发送 0 X、 4 X、 6 X、 8 X，CX，或 EX 类字节。 但是，该函数没有通过直接向 UICC 此字节。 相反，然后将 APDU 发送到 UICC 函数会从主机的第一个字节将替换为新类字节 (编码为定义的第四部分[ISO/IEC 7816-标准 4:2013](https://go.microsoft.com/fwlink/p/?linkid=864596)符或分节的 10.1.1 [ETSI TS102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)) 基于 host 所指定的类型、 通道和 SecureMessaging 值：

| 字节类 | 描述 |
| --- | --- |
| 0X | 7816 4 interindustry，1 < = 通道 < = 3，如果相关编码低位元组中的安全性 |
| 4X | 7816 4 interindustry，4 < = 通道 < = 19，不安全消息传送 |
| 6X | 7816 4 interindustry，4 < = 通道 < = 19，安全 （未经过身份验证标头） |
| 8X | 102 221 扩展，1 < = 通道 < = 3，如果相关编码低位元组中的安全性 |
| CX | 102 221 扩展，4 < = 通道 < = 19，不安全消息传送 |
| EX | 102 221 扩展，4 < = 通道 < = 19，安全 （未经过身份验证标头） |

该函数应返回状态、 SW1 SW2 和响应从 UICC 到主机。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_MS_SET_UICC_APDU | 不适用 | 不适用 |
| 响应 | MBIM_MS_UICC_APDU_INFO | 不适用 | 不适用 |

### <a name="query"></a>查询

不适用。

### <a name="set"></a>设置

MBIM_COMMAND_MSG InformationBuffer 包含以下 MBIM_MS_SET_UICC_APDU 结构。

#### <a name="mbimmssetuiccapdu"></a>MBIM_MS_SET_UICC_APDU

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 通道 | UINT32(1..19) | 指定用于发送 APDU 的通道。 |
| 4 | 4 | SecureMessaging | MBIM_MS_UICC_SECURE_MESSAGING | 指定是否使用安全消息交换 APDU。 |
| 8 | 4 | 在任务栏的搜索框中键入 | MBIM_MS_UICC_CLASS_BYTE_TYPE | 指定类字节定义的类型。 |
| 12 | 4 | CommandSize | UINT32(0..261) | **命令**长度以字节为单位。 |
| 16 | 4 | CommandOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到调用的字节数组**命令**，其中包含 APDU。 |
| 20 | - | DataBuffer | DATABUFFER | **命令**字节数组。 |

MBIM_MS_SET_UICC_APDU 结构使用以下 MBIM_MS_UICC_SECURE_MESSAGING 和 MBIM_MS_UICC_CLASS_BYTE_TYPE 数据结构。

##### <a name="mbimmsuiccsecuremessaging"></a>MBIM_MS_UICC_SECURE_MESSAGING

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMMsUiccSecureMessagingNone | 0 | 没有安全消息传送。 |
| MBIMMsUiccSecureMessagingNoHdrAuth | 1 | 安全消息传送，未经过身份验证的命令标头。 |

##### <a name="mbimmsuiccclassbytetype"></a>MBIM_MS_UICC_CLASS_BYTE_TYPE

| 在任务栏的搜索框中键入 | 值 | 描述 |
| --- | --- | --- |
| MBIMMsUiccInterindustry | 0 | ISO 7816 4 中的第一个 interindustry 定义根据定义。 |
| MBIMMsUiccExtended | 1 | ETSI 102 221 中的扩展定义根据定义。 |

### <a name="response"></a>响应

MBIM_COMMAND_DONE InformationBuffer 包含以下 MBIM_MS_UICC_APDU_INFO 结构。

#### <a name="mbimmsuiccapduinfo"></a>MBIM_MS_UICC_APDU_INFO

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状态 | BYTE[2] | 主机运行命令 SW1 和 SW2 状态字。 |
| 4 | 4 | ResponseLength | 大小 | 响应长度 （字节）。 |
| 8 | 4 | ResponseOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到调用的字节数组**响应**包含从选择的响应。 |
| 12 | - | DataBuffer | DATABUFFER | **响应**字节数组。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

下面的状态代码均适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 逻辑频道号不是有效 （即，它不打开与 MBIM_CID_MS_UICC_OPEN_CHANNEL）。 |

如果该函数可以将 APDU 发送到 UICC，它将返回 MBIM_STATUS_SUCCESS 以及 SW1 SW2 状态字和 UICC （如果有） 的响应。 主机必须检查的状态 (SW1 SW2) 来确定上 UICC APDU 命令是否已成功或失败的原因。

## <a name="mbimcidmsuiccterminalcapability"></a>MBIM_CID_MS_UICC_TERMINAL_CAPABILITY

主机发送 MBIM_CID_MS_UICC_TERMINAL_CAPABILITY 通知调制解调器有关主机的功能。 11.1.19 节中指定终端功能 APDU [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)，（如果支持），则选择第一个应用程序之前，必须向卡发送。 因此，该主机不能直接发送终端功能 APDU 但而是将发送 MBIM_CID_MS_UICC_TERMINAL_CAPABILITY 命令包含一个或多个终端的功能对象将调制解调器进行永久存储。 在下一步卡插入或重置之后 ATR，调制解调器将选择 MF 并检查是否支持终端功能。 如果是这样，调制解调器将发送终端功能 APDU MBIM_CID_MS_UICC_TERMINAL_CAPABILITY 命令，以及任何调制解调器生成信息由指定的信息。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_MS_SET_UICC_TERMINAL_CAPABILITY | 空 | 不适用 |
| 响应 | 不适用 | MBIM_MS_TERMINAL_CAPABILITY_INFO | 不适用 |

### <a name="query"></a>查询

InformationBuffer 应为 null，并且 InformationBufferLength 应该为零。

### <a name="set"></a>设置

MBIM_COMMAND_MSG InformationBuffer 包含以下 MBIM_MS_SET_UICC_TERMINAL_CAPABILITY 结构。

#### <a name="mbimmssetuiccterminalcapability"></a>MBIM_MS_SET_UICC_TERMINAL_CAPABILITY

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount | UINT32 | 终端的功能对象的元素计数。 |
| 4 | 8 * EC | CapabilityList OL_PAIR_LIST| 每个终端的功能对象 TLV 偏移量长度对列表。 |
| 4 + 8 * EC | - | DataBuffer | DATABUFFER | 实际的终端功能对象 TLVs 一个字节数组。 |

### <a name="response"></a>响应

响应将包含到调制解调器的最后一个发送终端功能对象的确切集命令。 因此，MBIM_MS_TERMINAL_CAPABILITY_INFO 等同于 MBIM_MS_SET_UICC_TERMINAL_CAPABILITY。

#### <a name="mbimmsterminalcapabilityinfo"></a>MBIM_MS_TERMINAL_CAPABILITY_INFO

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount | UINT32 | 终端的功能对象的元素计数。 |
| 4 | 8 * EC | CapabilityList OL_PAIR_LIST| 每个终端的功能对象 TLV 偏移量长度对列表。 |
| 4 + 8 * EC | - | DataBuffer | DATABUFFER | 实际的终端功能对象 TLVs 一个字节数组。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 逻辑频道号不是有效 （即，它不打开与 MBIM_CID_MS_UICC_OPEN_CHANNEL）。 |

## <a name="mbimcidmsuiccreset"></a>MBIM_CID_MS_UICC_RESET

主机将 MBIM_CID_MS_UICC_RESET 发送到 MBIM 函数将重置 UICC 或者将查询函数的传递状态。

当主机请求此功能重置 UICC 时，它指定传递操作。

如果指定了主机*MBIMMsUICCPassThroughEnable*传递操作，该函数将重置 UICC，并 UICC 加电时，将 UICC 像在直通模式下，可实现主机和 UICC （之间的通信即使 UICC 有没有电信 UICC 文件系统）。 该函数不会向卡发送任何 Apdu 并不会干扰任何时候在主机和 UICC 之间的通信。

如果指定了主机*MBIMMsUICCPassThroughDisable*传递操作，该函数将重置 UICC，UICC 加电时，将视为常规电信 UICC UICC 并且需要存在于 UICC 电信 UICC 文件系统.

当主机查询函数来确定传递状态，如果该函数使用响应*MBIMMsUICCPassThroughEnabled*状态，则表示启用该直通模式。 如果使用该函数响应*MBIMMsUICCPassThroughDisabled*状态，它表示该传递模式下处于禁用状态。

### <a name="parameters"></a>Parameters

|   | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_MS_SET_UICC_RESET | 空 | 不适用 |
| 响应 | MBIM_MS_UICC_RESET_INFO | MBIM_MS_UICC_RESET_INFO | 不适用 |

### <a name="query"></a>查询

InformationBuffer 应为空并*InformationBufferLength*应该为零。

### <a name="set"></a>设置

#### <a name="mbimsetmsuiccreset"></a>MBIM_SET_MS_UICC_RESET

MBIM_SET_MS_UICC_RESET 结构包含指定主机的传递操作。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PassThroughAction | MBIM_MS_UICC_PASSTHROUGH_ACTION | 有关详细信息，请参阅[MBIM_MS_UICC_PASSTHROUGH_ACTION](#mbim_ms_uicc_passthrough_action)。 |

#### <a name="mbimmsuiccpassthroughaction"></a>MBIM_MS_UICC_PASSTHROUGH_ACTION

MBIM_MS_UICC_PASSTHROUGH_ACTION 枚举定义 MBIM 函数传递操作，主机可以指定的类型。

| 类型 | ReplTest1 |
| --- | --- |
| MBIMMsUiccPassThroughDisable | 0 |
| MBIMMsUiccPassThroughEnable | 1 |

### <a name="response"></a>响应

#### <a name="mbimmsuiccresetinfo"></a>MBIM_MS_UICC_RESET_INFO

MBIM_MS_UICC_RESET_INFO 结构包含 MBIM 函数的传递状态。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PassThroughStatus | MBIM_MS_UICC_PASSTHROUGH_STATUS | 有关详细信息，请参阅[MBIM_MS_UICC_PASSTHROUGH_STATUS](#mbim_ms_uicc_passthrough_status)。 |

#### <a name="mbimmsuiccpassthroughstatus"></a>MBIM_MS_UICC_PASSTHROUGH_STATUS

MBIM_MS_UICC_PASSTHROUGH_STATUS 枚举定义主机的传递状态 MBIM 函数指定的类型。

| 类型 | ReplTest1 |
| --- | --- |
| MBIMMsUiccPassThroughDisabled | 0 |
| MBIMMsUiccPassThroughEnabled | 1 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_BUSY | 设备正在使用。 |
| MBIM_STATUS_FAILURE | 操作失败。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 设备不支持此操作。 |

### <a name="oidwwanuiccreset"></a>OID_WWAN_UICC_RESET

MBIM_CID_MS_UICC_RESET NDIS 等效项是[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)。 


