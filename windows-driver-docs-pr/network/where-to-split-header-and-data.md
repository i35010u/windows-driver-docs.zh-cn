---
title: 在何处拆分标头和数据
description: 在何处拆分标头和数据
ms.assetid: e302fcc1-5088-4f64-b454-5f20c69c0626
keywords:
- 标头数据拆分 WDK，拆分的位置
- 以太网帧拆分 WDK 网络、 拆分的位置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7288e9b056e0e569fb4980b877965cef30e8987d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365725"
---
# <a name="where-to-split-header-and-data"></a>在何处拆分标头和数据





以下是唯一有效位置标头数据拆分提供程序可以在何处拆分的以太网帧：

-   [大写层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

-   [UDP 负载的开头](splitting-frames-at-the-udp-payload.md)。

-   [TCP 有效负载的开头](splitting-frames-at-the-tcp-payload.md)。

**请注意**  这些要求仅适用于标头数据拆分提供程序。 有关拆分中不使用标头数据拆分的情况下的帧的详细信息，请参阅[情况下，标头数据拆分为不使用](cases-where-header-data-split-is-not-used.md)。

 

下图显示了以太网帧和有效的拆分位置的主要组成部分。

![说明通过 wep 算法加密 802.11 mpdu 帧的格式的关系图](images/hdsplitframe.png)

 

 





