---
title: MB 协议配置选项（PCO）操作
description: MB 协议配置选项（PCO）操作
ms.assetid: 682C507C-5B2C-45E3-99D2-EEC68F8FC715
keywords:
- MB PCO 选项，移动宽带 PCO 选项，MB 协议配置选项，移动宽带协议配置选项，WDK 网络驱动程序，MBB 微型端口驱动程序
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 833bb6114ad36b39a8080dff25988eead22efb7d
ms.sourcegitcommit: adccef85b24a37b1caa51e1b3435741a2f022cd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2020
ms.locfileid: "84724412"
---
# <a name="mb-protocol-configuration-options-pco-operations"></a>MB 协议配置选项（PCO）操作

## <a name="overview"></a>概述

用于协议配置选项（PCO）值的 Windows NDIS 定义通常是通用的，可能会在将来从调制解调器和网络接收完整的 PCO 值。 从 Windows 10 版本1709，某些调制解调器只能将操作员特定的 PCO 元素传递到 OS。 本主题定义当前操作员特定的 PCO 实现的行为。

在三种情况下，会将 PCO 值传递到主机：

- 新的 PCO 值到达激活的连接时
- 当应用程序或服务从调制解调器查询最新的 PCO 值时
- 首次桥接或激活连接时，在调制解调器中已经存在一个 PCO 值

在第一种情况下，在从网络接收新的 PCO 值时，该调制解调器应将[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)通知发送到操作系统，指示新的 PCO 值更改，并使用相应的 NDIS 端口号来表示相应的 PDN。 若要避免不必要地消耗电池，则调制解调器应避免发出干扰通知，如[使用选择性挂起和连接待机的调制解调器行为](#modem-behavior-with-selective-suspend-and-connected-standby)中所述。

在第二种情况下，当应用程序或服务在激活的 PDN 连接上从调制解调器查询 PCO 值时，主机将向调制解调器发送[OID_WWAN_PCO](oid-wwan-pco.md)查询请求，以读取调制解调器中的最新缓存 PCO 值。

在第三个方案中，当主机上的连接被激活或桥接时，如果在调制解调器中已经存在 PCO 值，则该调制解调器应发送**NDIS_STATUS_WWAN_PCO_STATUS**通知。 通知应从 PDN 的对应 NDIS 端口号向上传递。

下图显示了方案流：

![MB PCO 操作流](images/mb_PCO_operations_flow.png "MB PCO 操作流")

## <a name="modem-behavior-with-selective-suspend-and-connected-standby"></a>具有选择性挂起和连接备用的调制解调器行为

如果启用了 "选择性挂起"，则在接收到来自网络的 PCO 数据结构时，调制解调器可以通知操作系统。 但调制解调器应避免不必要的设备唤醒。 否则，来自网络的干扰 PCO 通知会频繁唤醒设备，并不必要地耗尽电池。

如果启用了连接待机，则调制解调器在从网络接收 PCO 数据结构时，不应通知 OS，因为它不仅会唤醒设备，还会唤醒操作系统，这并不是必需的。 相反，调制解调器应缓存数据结构中的所有最新的 PCO 元素，并在 OS 退出连接待机状态后通知操作系统。 对于 MBIM 调制解调器，它应缓存所有 PCO 数据结构，并且仅在主机订阅后将 PCO 通知发送到 OS。 当系统电源在连接待机后进入全功率状态后，将使用 MBIM_CID_DEVICE_SERVICE_SUBSCRIBE_LIST CID 完成此操作。

## <a name="resetting-the-modem-based-on-pco-values"></a>重置基于 PCO 值的调制解调器

根据从网络接收到的 PCO 值，将在以下情况下重置调制解调器：

- 用户在从网络接收 PCO = 5 之后完成自行激活。 新的 PCO 值（3，0或任何移动运营商应用可以识别的值）将发送到操作系统，操作系统会将其传递到移动运营商应用程序。
- 用户在收到 PCO = 3 后向其帐户添加了更多信用额度。 新的 PCO 值（0或任何移动运营商应用可以识别的值）将发送到操作系统，操作系统会将其传递到移动运营商应用。

主机无法识别正在重置的调制解调器，因此不会停用主机上的已激活连接，并且在重置后，调制解调器应该会自动重新建立与这些 PDN 的连接。 建立连接并从网络接收新的传入 PCO 值后，调制解调器将向主机提供未经请求的[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)通知。

下图说明了在发生其中一种情况时，该调制解调器的重置流，其中 Verizon 无线作为示例 MO：

![MB 基于 PCO 值的调制解调器重置](images/mb_PCO_modem_reset.png "MB 基于 PCO 值的调制解调器重置")

## <a name="ndis-interface-to-the-modem"></a>到调制解调器的 NDIS 接口

若要查询调制解调器从操作员网络接收的 PCO 值的状态和有效负载，请参阅[OID_WWAN_PCO](oid-wwan-pco.md)。 **OID_WWAN_PCO**使用[**NDIS_WWAN_PCO_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)结构，后者又包含表示来自网络的 PCO 信息负载的[**WWAN_PCO_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_pco_value)结构。

有关调制解调器微型驱动程序发送的状态通知，以将调制解调器的当前 PCO 状态通知给 OS，请参阅[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)。

## <a name="mb-cid-to-the-modem"></a>MB CID 到调制解调器

服务 = **MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**

服务 UUID = **3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

以下 Cid 是为 PCO 定义的：

| CID | 命令代码 | 最低操作系统版本 |
| --- | --- | --- |
| MBIM_CID_PCO | 9 | Windows 10 版本 1709 |

### <a name="mbim_cid_pco"></a>MBIM_CID_PCO

此命令用于查询从移动运营商网络缓存在调制解调器中的 PCO 数据。

#### <a name="query"></a>查询

InformationBuffer 包含唯一相关字段为*SessionId*的**MBIM_PCO_VALUE** 。 *SessionId*保留供将来使用，并且在 Windows 10 版本1709中将始终为0。 查询中的*SessionId*指示函数将返回哪个 IP 数据流的 PCO 值。

#### <a name="set"></a>设置

不适用。

#### <a name="unsolicited-event"></a>主动事件

未经请求的事件包含一个 MBIM_PCO_VALUE，并在新的 PCO 值到达激活的连接时发送。

#### <a name="parameters"></a>parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | MBIM_PCO_VALUE | 不适用 |
| 响应 | 不适用 | MBIM_PCO_VALUE | MBIM_PCO_VALUE |

#### <a name="data-structures"></a>数据结构

##### <a name="mbim_pco_type"></a>MBIM_PCO_TYPE

| 类型 | Value | 说明 |
| --- | --- | --- |
| MBIMPcoTypeComplete | 0 | 指定完整的 PCO 结构将在从网络接收的情况下传递，而标头实际反映在 3GPP TS 24.008 规范中定义的 PCO 结构的八进制3中的协议。 |
| MBIMPcoTypePartial | 1 | 指定该调制解调器将只传递从网络接收的 PCO 结构的一个子集。 标头与 3GPP TS 24.008 规范中定义的 PCO 结构相匹配，但八进制3的 "配置协议" 可能无效。 |

##### <a name="mbim-pco-type"></a>MBIM-PCO-TYPE

| Offset | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SessionId | UINT32 | 查询中的 SessionId 指示函数将返回哪个 IP 数据流的 PCO 值。 |
| 4 | 4 | PcoDataSize | UINT32 | PcoData 的长度（从0到256）。 在查询中，此值将为0。 |
| 8 | 4 | PcoDataType | UINT32 | PCO 数据类型。 有关详细信息，请参阅[MBIM_PCO_TYPE](#mbim_pco_type)。 |
| 12 | | PcoDataBuffer | DATABUFFER | 3GPP TS 24.008 规范中的 PCO 结构。 |

#### <a name="status-codes"></a>状态代码

此 CID 只使用一般状态代码。
