---
title: WDI 扩展通道切换通告 (ECSA)
description: '本部分提供了建议的驱动程序/固件更改，用于实现扩展通道交换机公告 (ECSA) '
ms.assetid: 9C59C8A2-335F-4BA4-8682-6DFFB82E1CAF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e08d3e36471d3dfefbac5bba26b8ec546a0d38f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216526"
---
# <a name="wdi-extended-channel-switch-announcement-ecsa"></a>WDI 扩展通道切换通告 (ECSA)


为了最大限度地减少 Wi-fi Direct 端口导致系统在多通道模式下运行的情况，多通道用例不像单通道用例那样高性能。 建议 (驱动程序/固件) 设备实现 ECSA。 此功能应完全存在于 IHV 端。

下面是建议的驱动程序/固件更改。

-   支持对 Wi-fi Direct 端口进行双向 ECSA。
-   如果设备是组所有者，并且处于多通道模式下：
    -   驱动程序必须检测远程对等机是否支持 ECSA。
    -   如果远程对等机支持 ECSA，请使用 ECSA 将对等互连到产生单个通道的通道配置。
-   如果设备是客户端并且处于多通道模式下：
    -   如果 ECSA 请求来自远程对等方，则支持该请求。
-   将通道更改通知发送到带有 [NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 组 \_ 操作 \_ 通道](./ndis-status-wdi-indication-p2p-group-operating-channel.md)的操作系统。

 

