---
title: 初始化使用预配上下文的 CDMA 数据包设备
description: 初始化使用预配上下文的 CDMA 数据包设备
ms.assetid: 07b4881c-b8df-4831-b0d3-521d187e4232
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 762b88cadd1f1b78f205e681903e8de57b3c2235
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212395"
---
# <a name="initialization-of-a-cdma-packet-device-with-a-provisioned-context"></a>初始化使用预配上下文的 CDMA 数据包设备


下图演示了基于 CDMA 的设备的最佳用户体验。 全新体验不需要用户配置。 此方案假定未激活基于 CDMA 的帐户。 与基于 GSM 的设备不同，在完成激活后，基于 CDMA 的设备会自动开始向网络注册。 粗体标签是 OID 标识符或事务流控制，而常规文本中的标签是 OID 结构中的重要标志。

![说明基于 cdma 的移动宽带-设备初始化序列的示意图](images/wwancdmadevinitseq.png)

若要使用预配的上下文初始化基于 CDMA 的数据包设备，请执行以下步骤：

1.  MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 就绪 \_ 信息](./oid-wwan-ready-info.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

2.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 失败发送 \_ 到 MB 服务。

3.  MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 服务 \_ 激活](./oid-wwan-service-activation.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

4.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

5.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 注册 \_ 状态**](./ndis-status-wwan-register-state.md) 发送到 MB 服务。

6.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 注册 \_ 状态**](./ndis-status-wwan-register-state.md) 发送到 MB 服务。

7.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](./ndis-status-wwan-packet-service.md) 发送到 MB 服务。

8.  MB 服务将异步 (非阻塞) [OID \_ WWAN \_ \_ 提供程序](./oid-wwan-home-provider.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

9.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

10. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 预配 \_ 上下文](./oid-wwan-provisioned-contexts.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

11. 微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

12. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 预配 \_ 上下文](./oid-wwan-provisioned-contexts.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

13. 微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

14. 微型端口驱动程序将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 发送到 MB 服务。

 

