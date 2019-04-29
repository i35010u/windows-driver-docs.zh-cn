---
title: 初始化非 SIM 锁定 GPRS 设备 （预配的上下文中）
description: SIM 锁定 GPRS 设备预配的上下文使用的初始化
ms.assetid: 0bbd4842-72ad-445b-9f28-b28e8740f263
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d218bcb55ff87903036f287ec1a0e414a64e4e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323392"
---
# <a name="initialization-of-a-non-sim-locked-gprs-device-with-a-provisioned-context"></a>SIM 锁定 GPRS 设备预配的上下文使用的初始化

下图表示基于 GSM 的 MB 设备的最佳用户体验。 开箱体验不需要用户配置。 假定该设备配置为自动选择要注册的网络。 粗体表示 OID 标识符或事务流控制中的标签和中常规文本的标签表示 OID 结构中的重要标志。

![说明基于 gsm 的 mb 设备初始化序列关系图](images/wwangsmdevinitseq.png)

若要初始化的 SIM 锁定基于 GSM 的设备，请执行以下步骤：

1.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_准备\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569833)微型端口驱动程序的查询请求来标识设备的就绪状态。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

2.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_准备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567856) MB 到指示的 MB 服务通知服务MB 设备的状态是**WwanReadyStateInitialized**。

3.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_注册\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569834)微型端口驱动程序的查询请求来标识设备的注册状态。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

4.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567857)到指示 MB 服务通知设备的注册模式是**WwanRegistraterModeAutomatic** ，且其当前注册状态不**WwanRegisterStateSearching**。

5.  更高版本，当设备注册到网络提供商，微型端口驱动程序发送未经请求的 NDIS\_状态\_WWAN\_注册\_状态通知指示 MB 服务当前设备的注册状态是**WwanRegisterStateHome**。

6.  设备尝试附加数据包服务。 当数据包服务状态更改为附加时，微型端口驱动程序将发送未经请求[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://msdn.microsoft.com/library/windows/hardware/ff567850)附加到 MB 服务，指示该数据包服务通知，并且当前的数据类**WWAN\_数据\_类\_GPRS**。

7.  MB 服务发送异步 （非阻塞） [OID\_WWAN\_家庭\_提供程序](https://msdn.microsoft.com/library/windows/hardware/ff569826)微型端口驱动程序的查询请求以检索家庭的提供程序的信息。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 这是已收到请求，它将会发送包含所需的信息在将来的通知。

8.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_家庭\_提供程序**](https://msdn.microsoft.com/library/windows/hardware/ff567848)指示家用供应商的 MB 服务通知详细信息。

9.  MB 服务发送异步 （非阻塞） OID\_WWAN\_已设置\_上下文查询请求到微型端口驱动程序来检索预配的上下文的列表。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

10. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_已预配\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff567854)到 MB 服务，其中包含一系列的通知[ **WWAN\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff571201)结构。

11. MB 服务发送异步 （非阻塞） [OID\_WWAN\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/ff569823)微型端口驱动程序集请求，若要激活数据包数据协议 (PDP) 上下文。 微型端口驱动程序会使用一个临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

12. 微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_上下文\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567843)指示该 PDP 上下文的 MB 服务通知已激活。

13. 微型端口驱动程序发送[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)通知以指示该媒体连接状态是**MediaConnectStateConnected**。

 

 





