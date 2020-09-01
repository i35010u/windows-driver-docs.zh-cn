---
title: WSDMON 端口监视器
description: WSDMON 端口监视器
ms.assetid: fd6b0136-ca6e-4882-b6b9-be868f0dfc18
keywords:
- 打印监视器 WDK，WSDMON
- WSDMON 端口监视器 WDK
- 端口监视 WDK 打印，WSDMON
- Web 服务设备 WDK WIA，端口监视器
- WSD 相容性 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dfc071efc24a31814fe735f26eae13424f73344
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205855"
---
# <a name="wsdmon-port-monitor"></a>WSDMON 端口监视器


WSDMON 端口监视器是一种打印机端口监视器，它支持打印到符合 [ (WSD) 技术的设备 Web 服务](./web-services-for-devices-print-service-schema.md)的网络打印机。 WSDMON 端口监视器侦听 WSD 事件，并相应地更新打印机状态。 此端口监视器是 Windows Vista 的新增端口。

WSDMON 端口监视器可以：

-   发现网络打印机并安装它们。

-   向 WSD 打印机发送作业。

-   监视 WSD 打印机的状态和配置，并相应地更新打印机对象状态。

-   为支持的 [双向架构](bidirectional-communication-schema.md)响应双向 (双向) 查询。

-   监视双向架构值更改并发送通知

WSDMON 的操作方式类似于 TCP/IP 端口监视器 ([TCPMON](tcpmon-xcv-interface.md)) 。 WSDMON 不支持以下 TCPMON 命令：

AddPort

DeletePort

MonitorUI

WSDMON 支持以下 Xcv 命令：

[CleanupPort](cleanupport.md)

[DeviceID](deviceid2.md)

[PnPXID](pnpxid.md)

[ResetCommunication](resetcommunication.md)

[ServiceID](serviceid.md)

有关适用于设备的 Web 服务的详细信息，请参阅 Microsoft Windows SDK 文档。

 

