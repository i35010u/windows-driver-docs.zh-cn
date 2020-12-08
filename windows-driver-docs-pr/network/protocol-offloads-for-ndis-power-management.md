---
title: NDIS 电源管理的协议卸载
description: NDIS 电源管理的协议卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6139fd53f466449b558c3eaeca9a5026d9c99306
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836719"
---
# <a name="protocol-offloads-for-ndis-power-management"></a>NDIS 电源管理的协议卸载





Ndis 6.20 和更高版本的 NDIS 支持 NDIS 电源管理的协议卸载。 例如，NDIS 可以将地址解析协议的处理 (ARP) 请求卸载到网络适配器。 某些应用程序使用定期 ARP 请求数据包来发现网络上的主机并确保其存在。 即使当前无需向主机发送数据，这些应用程序也会发送 ARP 请求。 此类 ARP 请求会唤醒主机，并在没有任何可用于宿主的情况时浪费电量。

**注意**   在 Windows 7 中，仅当绑定到微型端口适配器的所有协议和筛选器驱动程序支持 NDIS 6.20 和更高版本时，才会启用电源管理卸载功能。 在 Windows 8 中，如果微型端口适配器支持此功能，则会启用电源管理卸载功能，而不考虑协议和筛选器驱动程序的版本。

 

**注意**  如果传入数据包与卸载的协议和模式 (例如，由于配置错误) ，网络适配器将响应数据包并唤醒计算机。

 

为了最大程度地减少虚假唤醒，NDIS 协议驱动程序会尝试卸载对硬件的常用网络请求的响应。 某些网络协议要求主机定期公布特定信息。 如果网络适配器响应 ARP 请求，或接管协议特定的定期播发，而不会唤醒系统来处理这些请求，则可以避免很多虚假的唤醒事件。

有三种类型的低功率协议卸载：

-   IPv4 ARP

-    (NS) 的 IPv6 邻居请求

-   IEEE 802.11 稳健安全网络 (RSN) 4 向握手和双向握手

NDIS 允许多个协议驱动程序将不同的协议卸载到网络适配器。 为了确保在请求的协议解除次数高于网络适配器可支持的数目时卸载正确的协议集，协议驱动程序将优先级分配给每个协议卸载。 当由于网络适配器资源不足而导致 NDIS 无法添加新的高优先级协议卸载时，NDIS 可能会删除较低优先级的卸载。

有关管理协议卸载的详细信息，请参阅 [添加和删除低能耗协议卸载](adding-and-deleting-low-power-protocol-offloads.md)。

 

 





