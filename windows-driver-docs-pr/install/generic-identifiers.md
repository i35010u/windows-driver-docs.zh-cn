---
title: 通用标识符
description: 通用标识符
ms.assetid: 75dab2fc-e897-4bce-b719-98ad89817fca
keywords:
- 设备标识字符串 WDK，一般
- 标识字符串 WDK 设备，通用
- 标识符 WDK 设备，通用
- 一般设备标识符 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dbf665af3a9a7d76250a7b08ba16966f06cc1f5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095717"
---
# <a name="generic-identifiers"></a>通用标识符





大多数（但不是全部）标识符字符串都是特定于总线的。 即插即用 (PnP) 管理器还支持一组可在多个不同总线上出现的设备的通用设备标识符。 这些标识符的格式如下：

\*PNPd (4) 

其中 d (4) 是一个4位的十六进制类型标识符。

对于 PCMCIA 总线，以这种方式对兼容 Id 进行格式设置 (参阅 PCMCIA 总线) 的以下讨论。 可以在 Microsoft 下载中心的 [即插即用供应商 id 和设备 id](https://go.microsoft.com/fwlink/p/?linkid=49039) 中查找这些标识符的官方列表。 有关详细信息，请参阅 [即插即用 ID-PNPID 请求](./plug-and-play-id---pnpid-request.md) 。 

 

