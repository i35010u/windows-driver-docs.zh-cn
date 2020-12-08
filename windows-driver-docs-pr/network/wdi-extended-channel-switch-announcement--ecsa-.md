---
title: WDI 扩展通道切换通告 (ECSA)
description: '本部分提供了建议的驱动程序/固件更改，用于实现扩展通道交换机公告 (ECSA) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f4804ef7f66d3cc89a22f638569f4d6574c2ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822767"
---
# <a name="wdi-extended-channel-switch-announcement-ecsa"></a>WDI 扩展通道切换通告 (ECSA)


为了最大程度地降低 Wi-Fi 直接端口导致系统在多通道模式下运行的情况，多通道用例不像单通道用例那样高性能。 建议 (驱动程序/固件) 设备实现 ECSA。 此功能应完全存在于 IHV 端。

下面是建议的驱动程序/固件更改。

-   支持 Wi-Fi 直接端口上的双向 ECSA。
-   如果设备是组所有者，并且处于多通道模式下：
    -   驱动程序必须检测远程对等机是否支持 ECSA。
    -   如果远程对等机支持 ECSA，请使用 ECSA 将对等互连到产生单个通道的通道配置。
-   如果设备是客户端并且处于多通道模式下：
    -   如果 ECSA 请求来自远程对等方，则支持该请求。
-   将通道更改通知发送到带有 [NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 组 \_ 操作 \_ 通道](./ndis-status-wdi-indication-p2p-group-operating-channel.md)的操作系统。

 

