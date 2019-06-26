---
title: 数据包数据服务移交
description: 数据包数据服务移交
ms.assetid: 33cb68ac-42db-4bb0-8855-a8575e6e6331
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f846c3fd269132c891b4a99592642ddc8fd662a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376428"
---
# <a name="packet-data-service-handoffs"></a>数据包数据服务移交


下图显示了微型端口驱动程序数据包服务之间不同基于 GSM 的技术，如 GPRS、 EDGE、 UMTS、 HSDPA 或 TD SCDMA，移动或移动之间不同基于 CDMA 的技术，如 1xRTT，EV-不要时应遵循的步骤或 EV-不要 RevA。 以粗体显示的标签是 OID 标识符或事务流控制，并在常规文本的标签是 OID 结构中的重要标志。

![说明时数据包服务之间不同的基于 gsm 的技术移动微型端口驱动程序应遵循的步骤的关系图](images/wwanpacketdataservicehandoff.png)

请注意，除非在切换过程中发生更改的 IP 地址，MB 服务处理切换事件以透明方式而不会中断现有连接。 但是，微型端口驱动程序必须仍通知 MB 服务的媒体断开连接事件，当且仅当 IP 地址发生更改。

微型端口驱动程序和他们管理的 MB 设备应该能够处理第 2 层切换不同的无线接口之间自动，产生 MB 服务和其他叠加应用程序的最小影响。 唯一可能的影响是对可能会导致从技术移交的 IP 地址的更改。 在这种情况下，微型端口驱动程序应重新建立之前向 MB 服务报告数据包服务更改 MB 连接。 不会实现 DHCP 功能的微型端口驱动程序应使用[IP 帮助程序](ip-helper.md)关联[函数](https://docs.microsoft.com/windows-hardware/drivers/network/ip-helper)。 确实实现了 DHCP 功能的微型端口驱动程序不需要使用 IP 帮助程序函数，如以下关系图中所示。

若要将数据包数据服务提交，使用以下过程：

1.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)到 MB 服务。

2.  微型端口驱动程序将发送 NDIS\_WWAN\_链接\_MB 服务的状态。

3.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)到 MB 服务。

4.  微型端口驱动程序调用[ **DeleteUnicastIpAddressEntry** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546370(v=vs.85))与旧的 IP 地址的帮助器函数

5.  微型端口驱动程序调用[ **CreateUnicastIpAddressEntry** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546227(v=vs.85))使用新的 IP 地址的帮助器函数

6.  微型端口驱动程序发送[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)到 MB 服务。

7.  微型端口驱动程序发送[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)到 MB 服务。

8.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)到 MB 服务。

 

 





