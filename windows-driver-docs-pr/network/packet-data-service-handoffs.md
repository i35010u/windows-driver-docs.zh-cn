---
title: 数据包数据服务移交
description: 数据包数据服务移交
ms.assetid: 33cb68ac-42db-4bb0-8855-a8575e6e6331
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edb17f582cec67f387dcd203186d98e2bc3ce664
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207845"
---
# <a name="packet-data-service-handoffs"></a>数据包数据服务移交


下图显示了当数据包服务在不同的基于 GSM 的技术（如 GPRS、EDGE、UMTS、HSDPA 或 TD SCDMA）之间移动时，微型端口驱动程序应遵循的步骤，或在不同 CDMA 的技术之间移动（如1xRTT、EV 或 EV-DO RevA）。 粗体标签是 OID 标识符或事务流控制，而常规文本中的标签是 OID 结构中的重要标志。

![说明包服务在不同的基于 gsm 的技术之间移动时应遵循的步骤的示意图](images/wwanpacketdataservicehandoff.png)

请注意，除非 IP 地址在移交过程中发生更改，否则，MB 服务将透明地处理移交事件，而不会中断现有连接。 但是，如果且仅当 IP 地址发生变化时，微型端口驱动程序仍必须通知 MB 服务有关媒体断开连接事件的信息。

微型端口驱动程序和他们管理的 MB 设备应该能够自动处理不同无线接口之间的第2层切换，对 MB 服务和其他覆盖应用程序的影响最小。 唯一的影响可能是对技术移交可能导致的 IP 地址的更改。 在这种情况下，微型端口驱动程序应重新建立 MB 连接，然后将数据包服务更改报告给 MB 服务。 不实现 DHCP 功能的微型端口驱动程序应使用 [IP 帮助](ip-helper.md) 程序和关联的 [功能](./ip-helper.md)。 以下关系图中所示，无需使用 IP Helper 函数即可实现 DHCP 功能的微型端口驱动程序。

若要交付数据包数据服务，请使用以下过程：

1.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](./ndis-status-wwan-packet-service.md) 发送到 MB 服务。

2.  微型端口驱动程序将 NDIS \_ WWAN \_ 链接状态发送 \_ 到 MB 服务。

3.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](./ndis-status-wwan-packet-service.md) 发送到 MB 服务。

4.  微型端口驱动程序调用具有旧 IP 地址的 [**DeleteUnicastIpAddressEntry**](/previous-versions/windows/hardware/drivers/ff546370(v=vs.85)) helper 函数

5.  微型端口驱动程序调用 [**CreateUnicastIpAddressEntry**](/previous-versions/windows/hardware/drivers/ff546227(v=vs.85)) helper 函数和新的 IP 地址

6.  微型端口驱动程序将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 发送到 MB 服务。

7.  微型端口驱动程序将 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 发送到 MB 服务。

8.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](./ndis-status-wwan-packet-service.md) 发送到 MB 服务。

 

