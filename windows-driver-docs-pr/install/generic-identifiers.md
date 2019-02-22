---
title: 通用标识符
description: 通用标识符
ms.assetid: 75dab2fc-e897-4bce-b719-98ad89817fca
keywords:
- 设备标识字符串 WDK，泛型
- 标识字符串 WDK 设备泛型
- 标识符 WDK 设备泛型
- 通用设备标识符 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd70bbbf262ee75cd713ff4651a07c6321cc8189
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526493"
---
# <a name="generic-identifiers"></a>通用标识符





总线特定于大多数但并非所有标识符字符串。 插即用 (PnP) 管理器还支持可以出现在许多不同的总线的设备的一组通用设备标识符。 这些标识符是窗体：

\*PNPd(4)

其中 d(4) 是一个 4 位数字、 十六进制类型标识符。

PCMCIA 总线中，对于兼容 Id 的格式以这种方式 （请参阅 PCMCIA 总线以下讨论）。 您可以找到的官方列表中的这些标识符[即插即用和播放供应商 Id 和设备 Id](https://go.microsoft.com/fwlink/p/?linkid=49039)从 Microsoft 下载中心获得。 请参阅[插 ID-PNPID 请求](https://docs.microsoft.com/windows-hardware/drivers/install/plug-and-play-id---pnpid-request)有关详细信息。 

 

 





