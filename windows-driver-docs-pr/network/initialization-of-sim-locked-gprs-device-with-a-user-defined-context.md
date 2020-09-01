---
title: " (用户定义的上下文初始化 SIM 锁定的 GPRS 设备) "
description: 使用用户定义的上下文初始化 SIM 锁定的 GPRS 设备
ms.assetid: 655b7789-ffea-459c-9489-5c2f565b77ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eda30384b1bbc123b5353134c1b3d88cf4ff78a0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210733"
---
# <a name="initialization-of-sim-locked-gprs-device-with-a-user-defined-context"></a>使用用户定义的上下文初始化 SIM 锁定的 GPRS 设备


下图演示了用户输入 SIM PIN 并手动配置访问点名称字符串的情况。 粗体标签是 OID 标识符或事务流控制，而常规文本中的标签是 OID 结构中的重要标志。

![说明用户输入 sim pin 并手动配置访问点名称字符串的方案的关系图](images/wwanlockedgsmdevinitseq.png)

若要初始化 PIN1 锁定的基于 GSM 的设备，请执行以下步骤：

1.  MB 服务向微型端口驱动程序发送异步 (非阻塞) [OID \_ WWAN \_ 就绪 \_ 信息](./oid-wwan-ready-info.md) 查询请求，以标识设备的就绪状态。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

2.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 失败通知发送到 mb 服务，以向 mb 服务指明订阅服务器标识模块 (SIM) 锁定。

3.  MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 固定](./oid-wwan-pin.md) 查询请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

4.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 成功通知发送到 MB 服务。

5.  MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 固定](./oid-wwan-pin.md) 请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

6.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 成功通知发送到 MB 服务。

7.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 就绪 \_ 信息**](./ndis-status-wwan-ready-info.md) 通知发送到 mb 服务，该服务向 mb 服务指示 Mb 设备的状态为 " **WwanReadyStateInitialized**"。

8.  MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 注册 \_ 状态](./oid-wwan-register-state.md) 查询请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

9.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 成功通知发送到 MB 服务。

10. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 注册 \_ 状态**](./ndis-status-wwan-register-state.md) 通知发送到 MB 服务。

11. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ \_ 提供程序](./oid-wwan-home-provider.md) 查询请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

12. 微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 成功通知发送到 MB 服务。

13. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 注册 \_ 状态**](./ndis-status-wwan-register-state.md) 通知发送到 MB 服务。

14. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 数据包 \_ 服务](./oid-wwan-packet-service.md) 请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

15. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](./ndis-status-wwan-packet-service.md) 通知发送到 MB 服务。

16. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 预配 \_ 上下文](./oid-wwan-provisioned-contexts.md) 查询请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

17. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 预配 \_ 上下文**](./ndis-status-wwan-provisioned-contexts.md) 发送到 MB 服务。

18. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 预配 \_ 上下文](./oid-wwan-provisioned-contexts.md) 集请求发送到 MB 服务。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

19. 微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

 

