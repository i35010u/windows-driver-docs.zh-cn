---
title: WDI 扩展通道切换通告 (ECSA)
description: 本部分提供了建议的驱动程序/固件更改以实现扩展通道交换机公告 (ECSA)
ms.assetid: 9C59C8A2-335F-4BA4-8682-6DFFB82E1CAF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aea45a28acbb098ba0204b849c2dcbf5e62b27f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384340"
---
# <a name="wdi-extended-channel-switch-announcement-ecsa"></a>WDI 扩展通道切换通告 (ECSA)


若要最大程度减少其中 Wi-Fi Direct 端口将导致系统运行多渠道中的用例模式下，多渠道使用情况下不是作为单个通道的高性能为用例。 我们建议设备 （驱动程序/固件） 实现 ECSA。 此功能应完全位于 IHV 端。

以下是建议的驱动程序/固件的更改。

-   支持的双向 ECSA Wi-Fi Direct 端口上。
-   当设备是组所有者，并且是在多渠道模式下：
    -   该驱动程序必须检测到远程对等方是否支持 ECSA。
    -   如果远程对等方支持 ECSA，吸引 ECSA 可以移动对等方，以生成单通道的通道配置。
-   当设备是客户端，并且处于多渠道模式：
    -   如果 ECSA 请求来自远程对等方，然后支持它。
-   将通道更改通知发送到带有的操作系统[NDIS\_状态\_WDI\_指示\_P2P\_组\_操作系统\_通道](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-p2p-group-operating-channel).

 

 





