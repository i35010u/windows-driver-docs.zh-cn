---
title: " (预配的上下文初始化非 SIM 锁定的 GPRS 设备) "
description: 使用预配的上下文初始化非 SIM 锁定的 GPRS 设备
ms.assetid: 0bbd4842-72ad-445b-9f28-b28e8740f263
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bd66f44fa7cc97da2cc0a02e30bb709a075b81f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210744"
---
# <a name="initialization-of-a-non-sim-locked-gprs-device-with-a-provisioned-context"></a>使用预配的上下文初始化非 SIM 锁定的 GPRS 设备

下图表示基于 GSM 的 MB 设备的最佳用户体验。 全新体验不需要用户配置。 假定设备已配置为自动选择要向其注册的网络。 以粗体显示的标签表示 OID 标识符或事务流控制，而常规文本中的标签表示 OID 结构中的重要标志。

![演示基于 gsm 的 mb 设备初始化序列的示意图](images/wwangsmdevinitseq.png)

若要初始化非 SIM 锁定的基于 GSM 的设备，请执行以下步骤：

1.  MB 服务向微型端口驱动程序发送异步 (非阻塞) [OID \_ WWAN \_ 就绪 \_ 信息](./oid-wwan-ready-info.md) 查询请求，以标识设备的就绪状态。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

2.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 就绪 \_ 信息**](./ndis-status-wwan-ready-info.md) 通知发送到 mb 服务，该服务向 mb 服务指示 Mb 设备的状态为 " **WwanReadyStateInitialized**"。

3.  MB 服务向微型端口驱动程序发送异步 (非阻塞) [OID \_ WWAN \_ 注册 \_ 状态](./oid-wwan-register-state.md) 查询请求，以标识设备的注册状态。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

4.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 注册 \_ 状态**](./ndis-status-wwan-register-state.md) 通知发送到 MB 服务，该服务指示设备注册模式为 **WwanRegistraterModeAutomatic** ，其当前注册状态为 **WwanRegisterStateSearching**。

5.  稍后，在将设备注册到网络提供程序时，微型端口驱动程序将向 MB 服务发送未经请求的 NDIS \_ 状态 \_ WWAN \_ 注册 \_ 状态通知，这表示设备的当前注册状态为 " **WwanRegisterStateHome**"。

6.  设备尝试附加数据包服务。 当数据包服务状态更改为 "已连接" 时，微型端口驱动程序将向 MB 服务发送未经请求的 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](./ndis-status-wwan-packet-service.md) 通知，指示已附加数据包服务，当前数据类为 **WWAN \_ 数据 \_ 类 \_ GPRS**。

7.  MB 服务向微型端口驱动程序发送异步 (非阻塞) [OID \_ WWAN \_ \_ 提供程序](./oid-wwan-home-provider.md) 查询请求，以检索 HOME 提供程序信息。 微型端口驱动程序使用临时确认响应 (在 \_ \_ \_ 收到请求) 所需的 NDIS 状态指示，并在将来发送包含所需信息的通知。

8.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 主 \_ 提供程序**](./ndis-status-wwan-home-provider.md) 通知发送到 MB 服务，该服务指示 HOME 提供程序的详细信息。

9.  MB 服务向微型端口驱动程序发送异步 (非阻塞) OID \_ WWAN \_ 预配 \_ 上下文查询请求，以检索预配上下文的列表。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

10. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 预配 \_ 上下文**](./ndis-status-wwan-provisioned-contexts.md) 通知发送到 MB 服务，该服务包含一个 [**WWAN \_ 上下文**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_context) 结构列表。

11. MB 服务向微型端口驱动程序发送异步 (非阻塞) [OID \_ WWAN \_ 连接](./oid-wwan-connect.md) 集请求，以 (PDP) 上下文激活数据包数据协议。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

12. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 上下文 \_ 状态**](./ndis-status-wwan-context-state.md) 通知发送到 MB 服务，该服务指示激活了 PDP 上下文。

13. 微型端口驱动程序将发送一个 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 通知，以指示媒体连接状态为 " **MediaConnectStateConnected**"。

 

