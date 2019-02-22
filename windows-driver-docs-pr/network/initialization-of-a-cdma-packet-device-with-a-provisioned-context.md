---
title: CDMA 数据包设备预配的上下文使用的初始化
description: CDMA 数据包设备预配的上下文使用的初始化
ms.assetid: 07b4881c-b8df-4831-b0d3-521d187e4232
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec11d588984d99b13bda1d58525d8862e6274da2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525911"
---
# <a name="initialization-of-a-cdma-packet-device-with-a-provisioned-context"></a>CDMA 数据包设备预配的上下文使用的初始化


下图说明了基于 CDMA 的设备的最佳用户体验。 开箱体验不需要用户配置。 此方案假定尚未激活基于 CDMA 的帐户。 与不同的是基于 GSM 的设备，基于 CDMA 的设备会自动启动注册与网络完成激活后。 以粗体显示的标签是 OID 标识符或事务流控制，并在常规文本的标签是 OID 结构中的重要标志。

![说明基于 cdma 的移动宽带设备初始化序列关系图](images/wwancdmadevinitseq.png)

若要初始化基于 CDMA 的数据包设备与预配的上下文，请执行以下步骤：

1.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_准备\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569833)微型端口驱动程序。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

2.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务失败。

3.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_服务\_激活](https://msdn.microsoft.com/library/windows/hardware/ff569835)微型端口驱动程序。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

4.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

5.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567857)到 MB 服务。

6.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567857)到 MB 服务。

7.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://msdn.microsoft.com/library/windows/hardware/ff567850)到 MB 服务。

8.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_主页\_提供程序](https://msdn.microsoft.com/library/windows/hardware/ff569826)微型端口驱动程序。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

9.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

10. MB 服务发送异步 （非阻塞） [OID\_WWAN\_已预配\_上下文](https://msdn.microsoft.com/library/windows/hardware/ff569831)微型端口驱动程序。 微型端口驱动程序会使用临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

11. 微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

12. MB 服务发送异步 （非阻塞） [OID\_WWAN\_已预配\_上下文](https://msdn.microsoft.com/library/windows/hardware/ff569831)微型端口驱动程序。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

13. 微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

14. 微型端口驱动程序发送[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)到 MB 服务。

 

 





