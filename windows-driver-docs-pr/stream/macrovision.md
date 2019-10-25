---
title: Macrovision
description: Macrovision
ms.assetid: 62bd8d8a-3e58-4bca-a32d-ff792180afbe
keywords:
- DVD 解码器微型驱动程序 WDK，版权保护
- 解码器微型驱动程序 WDK DVD，版权保护
- 版权保护 WDK DVD 解码器
- Macrovision WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d997179f2af42c7896037d775cbf73cc3dc3461
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842139"
---
# <a name="macrovision"></a>Macrovision





在离开计算机之前处理视频数据的最后一个设备支持 Macrovision。 如果视频端口连接到视频卡，视频卡和 DVD 导航器/拆分器将处理所有 Macrovision 处理。 不涉及解码器。

如果解码器具有 NTSC 输出，则 Macrovision 编码和 Macrovision 符合性由解码器卡负责。 [**KS\_COPY\_MACROVISION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)属性指示媒体上的 MACROVISION 编码级别（级别0到3）。 解码器可能会使用此信息来启用或禁用针对 NTSC 输出的 Macrovision 编码。

 

 




