---
title: MB 协议配置选项 (PCO) 操作
description: MB 协议配置选项 (PCO) 操作
ms.assetid: 682C507C-5B2C-45E3-99D2-EEC68F8FC715
keywords:
- MB PCO 选项，移动宽带 PCO 选项 MB 协议配置选项、 移动宽带协议配置选项，WDK 网络驱动程序、 MBB 微型端口驱动程序
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: f149f51566190780a910ce6e876cf7ee420b8b66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543681"
---
# <a name="mb-protocol-configuration-options-pco-operations"></a>MB 协议配置选项 (PCO) 操作

## <a name="overview"></a>概述

一直以来，Windows NDIS 定义为协议配置选项 (PCO) 值已泛型类型，可能会在将来的调制解调器和网络从接收完整 PCO 值。 截至 Windows 10 版本 1709，但是，某些调制解调器是仅能够将沿运算符特定 PCO 元素向上传递到 OS。 本主题定义当前运算符仅特定于 PCO 实现的行为。

有三种方案，其中 PCO 值将传递到主机：
1.  新的 PCO 值时到达的激活连接
2.  当应用或服务查询从调制解调器的最新 PCO 值
3.  当桥接连接或已激活的第一次和 PCO 值存在于调制解调器

对于第一个方案，应将发送调制解调器[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)到 OS 从网络具有合适的 NDIS 端口号为接收新 PCO 值时，指示新 PCO 值发生了更改的通知表示相应 PDN。 若要避免不必要地消耗电池，调制解调器应避免干扰性通知，如中所述[调制解调器的选择性挂起和连接待机行为](#modem-behavior-with-selective-suspend-and-connected-standby)。

对于第二个方案中，当从激活 PDN 连接调制解调器 PCO 值应用或服务查询主机将发送调制解调器[OID_WWAN_PCO](oid-wwan-pco.md)中阅读最新的查询请求缓存中的调制解调器 PCO 值。

对于第三个方案中，当激活或在主机上，桥接连接调制解调器应发送**NDIS_STATUS_WWAN_PCO_STATUS** PCO 值中的激活或桥接连接的调制解调器已存在时的通知请求的主机。 应从对应的 NDIS 端口号的 PDN 传递通知。

下图显示的方案流：

![MB PCO 操作流](images/mb_PCO_operations_flow.png "MB PCO 操作流")

## <a name="modem-behavior-with-selective-suspend-and-connected-standby"></a>调制解调器行为的选择性挂起和连接待机

启用选择性挂起后，调制解调器可以通知操作系统，每当它收到来自网络 PCO 数据结构时。 但是，调制解调器应避免不必要的设备唤醒。 否则为从网络干扰 PCO 通知将经常唤醒设备并不必要地消耗电池。

启用连接待机，调制解调器不应通知操作系统时它从网络接收 PCO 数据结构，因为它不仅会唤醒设备，而且还将唤醒的操作系统不是必需的。 相反，调制解调器应缓存的数据结构中的所有最新 PCO 元素和 OS 退出连接待机后通知操作系统。 对于 MBIM 调制解调器，它应缓存所有 PCO 数据结构，并仅将 PCO 通知发送到 OS 后主机已进行订阅。 这会在系统电源已连接待机出传入后返回到完整功能时使用 MBIM_CID_DEVICE_SERVICE_SUBSCRIBE_LIST CID。

## <a name="resetting-the-modem-based-on-pco-values"></a>重置 PCO 值为基础的调制解调器

基于从网络接收的 PCO 值，将在以下情况下重置调制解调器：

1.  用户完成自我激活接收 PCO 后的 = 5 从网络。 新的 PCO 值 （3、 0 或任何内容移动运营商应用程序可以识别） 将发送到操作系统和操作系统会将其传递给移动运营商应用程序。
2.  将用户添加更多信用额度为其帐户后接收 PCO = 3。 新的 PCO 值 （0，或任何内容移动运营商应用程序可以识别） 将发送到操作系统和操作系统会将其传递给移动运营商应用程序。

主机并不知道正在重置，因此未停用来自主机激活的连接和调制解调器应自动重新建立与这些 PDN 后重置连接的调制解调器。 在建立连接并从网络接收新的传入 PCO 值，将提供未经请求的调制解调器[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)到主机的通知。

下图演示了其中一种情形发生，使用如月 Verizon 无线使用调制解调器的重置流：

![MB 调制解调器基于 PCO 值重置](images/mb_PCO_modem_reset.png "MB 调制解调器基于 PCO 值重置")

## <a name="ndis-interface-to-the-modem"></a>到调制解调器的 NDIS 接口

有关查询的状态和负载的 PCO 值从运营商网络接收的调制解调器，请参阅[OID_WWAN_PCO](oid-wwan-pco.md)。 **OID_WWAN_PCO**使用[ **NDIS_WWAN_PCO_STATUS** ](https://msdn.microsoft.com/library/windows/hardware/C71187C5-74B6-450A-8461-BB9FDF60DB8D)结构，其中又包含[ **WWAN_PCO_VALUE** ](https://msdn.microsoft.com/library/windows/hardware/45A499CE-2C9A-4070-BEF8-880E7673FA8E) 从网络表示 PCO 信息有效负载的结构。

有关调制解调器微型端口驱动程序发送通知的调制解调器中的当前 PCO 状态的操作系统的状态通知，请参阅[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)。

## <a name="mb-cid-to-the-modem"></a>MB CID 到调制解调器

Service = **MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**

Service UUID = **3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

为 PCO 定义以下 Cid:

| CID | 命令代码 | 最低 OS 版本 |
| --- | --- | --- |
| MBIM_CID_PCO | 9 | Windows 10 版本 1709 |

### <a name="mbimcidpco"></a>MBIM_CID_PCO

此命令用于查询调制解调器从移动运营商网络中缓存的 PCO 数据。

#### <a name="query"></a>查询

包含 InformationBuffer **MBIM_PCO_VALUE**中仅相关字段即*SessionId*。 *SessionId*是保留供将来使用，将始终为 0 于 Windows 10，版本 1709年。 *SessionId*在查询中指示的 IP 数据流 PCO 值是由函数返回。 

#### <a name="set"></a>设置

不适用。

#### <a name="unsolicited-event"></a>未经请求的事件

未经请求的事件包含 MBIM_PCO_VALUE 和新 PCO 值到达的激活连接时发送。

#### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | MBIM_PCO_VALUE | 不适用 |
| 响应 | 不适用 | MBIM_PCO_VALUE | MBIM_PCO_VALUE |

#### <a name="data-structures"></a>数据结构

##### <a name="mbimpcotype"></a>MBIM_PCO_TYPE

| 在任务栏的搜索框中键入 | 值 | 描述 |
| --- | --- | --- |
| MBIMPcoTypeComplete | 0 | 指定完整的 PCO 结构将向上传递，如从网络接收和标头真实地反映了在 PCO 结构八位字节 3 3GPP TS24.008 规范中定义的协议。 |
| MBIMPcoTypePartial | 1 | 指定调制解调器将只传递了 PCO 结构，它从网络接收的子集。 标头匹配 PCO 结构定义中 3GPP TS24.008 规范，但可能不是有效的八位位组 3 的"配置协议"。 |

##### <a name="mbimpcovalue"></a>MBIM_PCO_VALUE

| 偏移量 | 尺寸 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SessionId | UINT32 | 在查询中的 SessionId 指示哪些 IP 数据流 PCO 值是由函数返回。 |
| 4 | 4 | PcoDataSize | UINT32 | 从 0 到 256 的 PcoData，长度。 此值将为在查询中的 0。 |
| 8 | 4 | PcoDataType | UINT32 | PCO 数据类型。 有关详细信息，请参阅[MBIM_PCO_TYPE](#mbimpcotype)。 |
| 12 | | PcoDataBuffer | DATABUFFER | 3GPP TS24.008 规范中 PCO 结构。 |

#### <a name="status-codes"></a>状态代码

此 CID 仅使用常规状态代码。
