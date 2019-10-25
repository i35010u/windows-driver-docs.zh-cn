---
title: 初始化非 SIM 锁定的 GPRS 设备（预配的上下文）
description: 使用预配的上下文初始化非 SIM 锁定的 GPRS 设备
ms.assetid: 0bbd4842-72ad-445b-9f28-b28e8740f263
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9778138857212745a4d9e9d57c1fa56eef91cf11
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824614"
---
# <a name="initialization-of-a-non-sim-locked-gprs-device-with-a-provisioned-context"></a>使用预配的上下文初始化非 SIM 锁定的 GPRS 设备

下图表示基于 GSM 的 MB 设备的最佳用户体验。 全新体验不需要用户配置。 假定设备已配置为自动选择要向其注册的网络。 以粗体显示的标签表示 OID 标识符或事务流控制，而常规文本中的标签表示 OID 结构中的重要标志。

![演示基于 gsm 的 mb 设备初始化序列的示意图](images/wwangsmdevinitseq.png)

若要初始化非 SIM 锁定的基于 GSM 的设备，请执行以下步骤：

1.  MB 服务向微型端口驱动程序发送异步（非阻塞） [OID\_WWAN\_就绪\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)查询请求，以标识设备的就绪状态。 微型端口驱动程序使用临时确认（NDIS\_状态\_指示\_必需）收到请求，并向将来发送请求的信息。

2.  微型端口驱动程序将[**NDIS\_状态\_WWAN\_就绪\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)通知发送到 mb 服务，该服务向 mb 服务指示 mb 设备的状态**WwanReadyStateInitialized**。

3.  MB 服务向微型端口驱动程序发送异步（非阻塞） [OID\_WWAN\_注册\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)查询请求，以标识设备的注册状态。 微型端口驱动程序使用临时确认（NDIS\_状态\_指示\_必需）收到请求，并向将来发送请求的信息。

4.  微型端口驱动程序将[**NDIS\_状态\_WWAN\_注册\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)通知发送到 MB 服务，该服务指示设备注册模式为**WwanRegistraterModeAutomatic**及其当前注册状态为**WwanRegisterStateSearching**。

5.  稍后，在将设备注册到网络提供程序时，微型端口驱动程序会将未经请求的 NDIS\_状态发送\_WWAN\_REGISTER\_状态通知发送到 MB 服务，该服务指示当前的注册状态设备为**WwanRegisterStateHome**。

6.  设备尝试附加数据包服务。 当数据包服务状态更改为 "已连接" 时，微型端口驱动程序会将未经请求的[**NDIS\_状态\_WWAN\_数据包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)通知发送到 MB 服务，该服务指示已附加数据包服务，当前数据类为**WWAN\_数据\_类\_GPRS**。

7.  MB 服务向微型端口驱动程序[\_WWAN\_HOME\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)查询请求发送异步（非阻塞） OID，以检索 HOME 提供程序信息。 微型端口驱动程序会使用已收到请求的临时确认（NDIS\_状态\_指示\_必需）进行响应，并且它将在将来发送包含所需信息的通知。

8.  微型端口驱动程序将一个[**NDIS\_状态\_WWAN\_HOME\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)通知发送到表示 HOME 提供程序详细信息的 MB 服务。

9.  MB 服务将\_WWAN\_预配\_上下文查询请求的异步（非阻塞） OID 发送到微型端口驱动程序，以检索预配的上下文列表。 微型端口驱动程序使用临时确认（NDIS\_状态\_指示\_必需）收到请求，并向将来发送请求的信息。

10. 微型端口驱动程序将[**NDIS\_状态\_wwan\_预配\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)通知发送到 MB 服务，该服务包含一个[**WWAN\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_context)结构列表。

11. MB 服务将异步（非阻塞） [OID\_WWAN\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect) set 请求发送到微型端口驱动程序，以激活数据包数据协议（PDP）上下文。 微型端口驱动程序使用临时确认（NDIS\_状态\_指示\_必需）收到请求，并向将来发送请求的信息。

12. 微型端口驱动程序将[**NDIS\_状态\_WWAN\_上下文\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)通知发送到 MB 服务，该服务指示激活了 PDP 上下文。

13. 微型端口驱动程序将[**NDIS\_状态发送\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)通知，以指示媒体连接状态为**MediaConnectStateConnected**。

 

 





