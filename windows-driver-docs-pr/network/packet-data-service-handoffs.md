---
title: 数据包数据服务移交
description: 数据包数据服务移交
ms.assetid: 33cb68ac-42db-4bb0-8855-a8575e6e6331
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 336d0a23441ce5cd7f6983b98661548bc8c90d62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523556"
---
# <a name="packet-data-service-handoffs"></a>数据包数据服务移交


下图显示了微型端口驱动程序数据包服务之间不同基于 GSM 的技术，如 GPRS、 EDGE、 UMTS、 HSDPA 或 TD SCDMA，移动或移动之间不同基于 CDMA 的技术，如 1xRTT，EV-不要时应遵循的步骤或 EV-不要 RevA。 以粗体显示的标签是 OID 标识符或事务流控制，并在常规文本的标签是 OID 结构中的重要标志。

![说明时数据包服务之间不同的基于 gsm 的技术移动微型端口驱动程序应遵循的步骤的关系图](images/wwanpacketdataservicehandoff.png)

请注意，除非在切换过程中发生更改的 IP 地址，MB 服务处理切换事件以透明方式而不会中断现有连接。 但是，微型端口驱动程序必须仍通知 MB 服务的媒体断开连接事件，当且仅当 IP 地址发生更改。

微型端口驱动程序和他们管理的 MB 设备应该能够处理第 2 层切换不同的无线接口之间自动，产生 MB 服务和其他叠加应用程序的最小影响。 唯一可能的影响是对可能会导致从技术移交的 IP 地址的更改。 在这种情况下，微型端口驱动程序应重新建立之前向 MB 服务报告数据包服务更改 MB 连接。 不会实现 DHCP 功能的微型端口驱动程序应使用[IP 帮助程序](ip-helper.md)关联[函数](https://msdn.microsoft.com/library/windows/hardware/ff557018)。 确实实现了 DHCP 功能的微型端口驱动程序不需要使用 IP 帮助程序函数，如以下关系图中所示。

若要将数据包数据服务提交，使用以下过程：

1.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://msdn.microsoft.com/library/windows/hardware/ff567850)到 MB 服务。

2.  微型端口驱动程序将发送 NDIS\_WWAN\_链接\_MB 服务的状态。

3.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://msdn.microsoft.com/library/windows/hardware/ff567850)到 MB 服务。

4.  微型端口驱动程序调用[ **DeleteUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff546370)与旧的 IP 地址的帮助器函数

5.  微型端口驱动程序调用[ **CreateUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff546227)使用新的 IP 地址的帮助器函数

6.  微型端口驱动程序发送[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)到 MB 服务。

7.  微型端口驱动程序发送[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)到 MB 服务。

8.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://msdn.microsoft.com/library/windows/hardware/ff567850)到 MB 服务。

 

 





