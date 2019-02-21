---
title: NDIS 电源管理的协议卸载
description: NDIS 电源管理的协议卸载
ms.assetid: 191aa59d-1772-4824-ad15-e813f2e154e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea4f1904bac0bccc9011a0587eb339edf3c51d14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522346"
---
# <a name="protocol-offloads-for-ndis-power-management"></a>NDIS 电源管理的协议卸载





NDIS 6.20 和更高版本的 NDIS NDIS 电源管理的支持协议卸载。 例如，NDIS 可以卸载到的网络适配器的地址解析协议 (ARP) 请求的处理。 某些应用程序使用定期 ARP 请求数据包来发现并确保在网络上的主机存在。 即使在没有当前需要将数据发送到主机时，这些应用程序发送 ARP 请求。 此类 ARP 请求唤醒主机并浪费电源时没有任何主机来执行操作。

**请注意**  在 Windows 7，电源管理卸载功能时，才启用所有协议和筛选器驱动程序绑定到的微型端口适配器都支持 NDIS 6.20 和更高版本。 在 Windows 8 中，如果微型端口适配器支持此功能，而不考虑协议和筛选器驱动程序版本启用电源管理卸载功能。

 

**请注意**  网络适配器的传入数据包与卸载的协议和模式匹配 （例如，由于配置错误），如果响应数据包并唤醒计算机。

 

若要尽量减少虚假唤醒 ups，尝试卸载到硬件的常用的网络请求响应协议的 NDIS 驱动程序。 某些网络协议要求主机将定期播发的特定信息。 当网络适配器响应 ARP 请求，或将接管协议特定的定期播发，而无需唤醒系统，用于处理这些请求时，可以避免很多虚假唤醒事件。

有三种类型的低能耗协议卸载：

-   IPv4 ARP

-   IPv6 邻居请求 (NS)

-   IEEE 802.11 可靠安全的网络 (RSN) 4 路和 2 路握手

NDIS 允许多个协议驱动程序来卸载不同协议的网络适配器。 若要确保正确的协议集卸载请求的协议卸载数高于网络适配器可以支持的数字时，协议驱动程序分配到每个协议卸载的优先级。 在 NDIS 不能添加新的高优先级协议卸载因为网络适配器的资源不足，可能会删除 NDIS 时将卸载较低的优先级。

对卸载管理协议详细信息，请参阅[添加和删除低电源协议卸载](adding-and-deleting-low-power-protocol-offloads.md)。

 

 





