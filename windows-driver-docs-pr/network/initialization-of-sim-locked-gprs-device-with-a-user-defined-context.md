---
title: 初始化 SIM 锁定 GPRS 设备 （用户定义的上下文）
description: SIM 锁定 GPRS 设备与用户定义的上下文的初始化
ms.assetid: 655b7789-ffea-459c-9489-5c2f565b77ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc79ad5fa8939f99701af906a45e6b432bb5df9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379837"
---
# <a name="initialization-of-sim-locked-gprs-device-with-a-user-defined-context"></a>SIM 锁定 GPRS 设备与用户定义的上下文的初始化


下图说明了用户输入 SIM PIN 和手动配置的访问点名称字符串的方案。 以粗体显示的标签是 OID 标识符或事务流控制，并在常规文本的标签是 OID 结构中的重要标志。

![说明用户输入 sim pin 和手动配置的访问点名称字符串的方案的关系图](images/wwanlockedgsmdevinitseq.png)

若要使用 PIN1 锁定初始化基于 GSM 的设备，请执行以下步骤：

1.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_准备\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569833)微型端口驱动程序的查询请求来标识设备的就绪状态。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

2.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务故障通知，以指示到 MB 服务已锁定用户识别模块 (SIM)。

3.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_PIN](https://msdn.microsoft.com/library/windows/hardware/ff569828)微型端口驱动程序的查询请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

4.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务的成功通知。

5.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_PIN](https://msdn.microsoft.com/library/windows/hardware/ff569828)微型端口驱动程序集请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

6.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务的成功通知。

7.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_准备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567856) MB 到指示的 MB 服务通知服务MB 设备的状态是**WwanReadyStateInitialized**。

8.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_注册\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569834)微型端口驱动程序的查询请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

9.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务的成功通知。

10. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567857) MB 服务的通知。

11. MB 服务发送异步 （非阻塞） [OID\_WWAN\_主页\_提供程序](https://msdn.microsoft.com/library/windows/hardware/ff569826)微型端口驱动程序的查询请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

12. 微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务的成功通知。

13. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567857) MB 服务的通知。

14. MB 服务发送异步 （非阻塞） [OID\_WWAN\_数据包\_服务](https://msdn.microsoft.com/library/windows/hardware/ff569827)微型端口驱动程序的请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

15. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://msdn.microsoft.com/library/windows/hardware/ff567850) MB 服务的通知。

16. MB 服务发送异步 （非阻塞） [OID\_WWAN\_已预配\_上下文](https://msdn.microsoft.com/library/windows/hardware/ff569831)微型端口驱动程序的查询请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

17. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_已预配\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff567854)到 MB 服务。

18. MB 服务发送异步 （非阻塞） [OID\_WWAN\_已预配\_上下文](https://msdn.microsoft.com/library/windows/hardware/ff569831)MB 服务集请求。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

19. 微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

 

 





