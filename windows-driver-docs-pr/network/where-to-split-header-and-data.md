---
title: 在何处拆分标头和数据
description: 在何处拆分标头和数据
keywords:
- 标头-数据拆分 WDK，要拆分的位置
- 用于拆分 WDK 网络的以太网帧，要拆分的位置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c341e74432e6c8174a7f2edde5f322b7610908d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821877"
---
# <a name="where-to-split-header-and-data"></a>在何处拆分标头和数据





下面是标题-数据拆分提供程序可在其中拆分以太网帧的唯一有效位置：

-   [上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

-   [UDP 有效负载的开头](splitting-frames-at-the-udp-payload.md)。

-   [TCP 有效负载的开头](splitting-frames-at-the-tcp-payload.md)。

**注意**  这些要求仅适用于标头-数据拆分提供程序。 有关在不使用标头数据拆分的情况下拆分框架的详细信息，请参阅 [不使用 Header-Data 拆分的情况](cases-where-header-data-split-is-not-used.md)。

 

下图显示了以太网帧和有效拆分位置的主要部分。

![说明通过 wep 算法加密的 802.11 mpdu 帧格式的关系图](images/hdsplitframe.png)

 

 





