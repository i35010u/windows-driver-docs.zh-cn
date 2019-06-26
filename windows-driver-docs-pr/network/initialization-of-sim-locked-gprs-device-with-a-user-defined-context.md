---
title: 初始化 SIM 锁定 GPRS 设备 （用户定义的上下文）
description: SIM 锁定 GPRS 设备与用户定义的上下文的初始化
ms.assetid: 655b7789-ffea-459c-9489-5c2f565b77ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c1846a5dd7b4518542a1b1e26c21313e028bf5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385090"
---
# <a name="initialization-of-sim-locked-gprs-device-with-a-user-defined-context"></a>SIM 锁定 GPRS 设备与用户定义的上下文的初始化


下图说明了用户输入 SIM PIN 和手动配置的访问点名称字符串的方案。 以粗体显示的标签是 OID 标识符或事务流控制，并在常规文本的标签是 OID 结构中的重要标志。

![说明用户输入 sim pin 和手动配置的访问点名称字符串的方案的关系图](images/wwanlockedgsmdevinitseq.png)

若要使用 PIN1 锁定初始化基于 GSM 的设备，请执行以下步骤：

1.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_准备\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)微型端口驱动程序的查询请求来标识设备的就绪状态。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

2.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务故障通知，以指示到 MB 服务已锁定用户识别模块 (SIM)。

3.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)微型端口驱动程序的查询请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

4.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务的成功通知。

5.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)微型端口驱动程序集请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

6.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务的成功通知。

7.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_准备\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info) MB 到指示的 MB 服务通知服务MB 设备的状态是**WwanReadyStateInitialized**。

8.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_注册\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)微型端口驱动程序的查询请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

9.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务的成功通知。

10. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_注册\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state) MB 服务的通知。

11. MB 服务发送异步 （非阻塞） [OID\_WWAN\_主页\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)微型端口驱动程序的查询请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

12. 微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务的成功通知。

13. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_注册\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state) MB 服务的通知。

14. MB 服务发送异步 （非阻塞） [OID\_WWAN\_数据包\_服务](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service)微型端口驱动程序的请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

15. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service) MB 服务的通知。

16. MB 服务发送异步 （非阻塞） [OID\_WWAN\_已预配\_上下文](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)微型端口驱动程序的查询请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

17. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_已预配\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)到 MB 服务。

18. MB 服务发送异步 （非阻塞） [OID\_WWAN\_已预配\_上下文](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)MB 服务集请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

19. 微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

 

 





