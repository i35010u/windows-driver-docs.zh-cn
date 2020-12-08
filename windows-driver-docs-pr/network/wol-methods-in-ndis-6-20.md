---
title: NDIS 6.20 中的 WOL 方法
description: NDIS 6.20 中的 WOL 方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 407ba141772958276e8a1283bbf1e9a4780edbf4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836199"
---
# <a name="wol-methods-in-ndis-620"></a>NDIS 6.20 中的 WOL 方法





Ndis 6.20 和更高版本的 NDIS 支持的电源管理功能由以下 LAN 唤醒 (WOL) 方法组成：

-   幻数据包唤醒

-   模式匹配时唤醒

-   Media connect 上的唤醒设备

有关以前版本的 Windows 中的电源管理功能的详细信息，请参阅 [电源管理 (NDIS 6.0 和更高版本) ](ndis-power-management-overview.md)。

当网络适配器收到 *幻数据包* 时，*幻数据包唤醒* 方法唤醒计算机。 *幻数据包* 包含接收网络适配器的以太网地址的16个连续副本。

" *对幻数据包唤醒* " 方法与 " *唤醒模式匹配* " 方法不同。 WOL 模式包含其他数据包类型或位图。 有关 WOL 模式的详细信息，请参阅 [用于 NDIS 电源管理的 WOL 模式](wol-patterns-for-ndis-power-management.md)。

尽管某些网络适配器为 *media connect 方法上的唤醒设备* 报告支持，但以前版本的 Windows 不支持。 如果 NDIS 6.20 微型端口驱动程序报告支持，Windows 7 完全支持 *在 media connect 方法上唤醒设备* 。 如果媒体断开连接，NDIS 会将网络适配器设置为低功率状态。

有关在 *media connect 方法上唤醒设备* 的详细信息，请参阅 [低能耗媒体断开](low-power-on-media-disconnect.md)连接。

 

 





