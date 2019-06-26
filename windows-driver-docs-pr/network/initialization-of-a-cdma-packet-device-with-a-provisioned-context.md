---
title: 初始化使用预配上下文的 CDMA 数据包设备
description: 初始化使用预配上下文的 CDMA 数据包设备
ms.assetid: 07b4881c-b8df-4831-b0d3-521d187e4232
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52c91035decbb18fe6ec23b264987685bc0d307a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385093"
---
# <a name="initialization-of-a-cdma-packet-device-with-a-provisioned-context"></a>初始化使用预配上下文的 CDMA 数据包设备


下图说明了基于 CDMA 的设备的最佳用户体验。 开箱体验不需要用户配置。 此方案假定尚未激活基于 CDMA 的帐户。 与不同的是基于 GSM 的设备，基于 CDMA 的设备会自动启动注册与网络完成激活后。 以粗体显示的标签是 OID 标识符或事务流控制，并在常规文本的标签是 OID 结构中的重要标志。

![说明基于 cdma 的移动宽带设备初始化序列关系图](images/wwancdmadevinitseq.png)

若要初始化基于 CDMA 的数据包设备与预配的上下文，请执行以下步骤：

1.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_准备\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)微型端口驱动程序。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

2.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_到 MB 服务失败。

3.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_服务\_激活](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-service-activation)微型端口驱动程序。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

4.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

5.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_注册\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)到 MB 服务。

6.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_注册\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)到 MB 服务。

7.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)到 MB 服务。

8.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_主页\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)微型端口驱动程序。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

9.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

10. MB 服务发送异步 （非阻塞） [OID\_WWAN\_已预配\_上下文](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)微型端口驱动程序。 微型端口驱动程序会使用临时确认进行响应 (NDIS\_状态\_指示\_必需) 已收到请求，并将发送包含所需的信息在将来的通知。

11. 微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

12. MB 服务发送异步 （非阻塞） [OID\_WWAN\_已预配\_上下文](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)微型端口驱动程序。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

13. 微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

14. 微型端口驱动程序发送[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)到 MB 服务。

 

 





