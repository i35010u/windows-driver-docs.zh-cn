---
title: Storport i/o 模型概述
description: Storport i/o 模型概述
ms.assetid: 9220b01e-725f-4a03-87f1-402c0686cccd
keywords:
- Storport 驱动程序 WDK，i/o
- I/o WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ee4cd96f3c8d5e294ab1e1f261b4ddcbccc9dec
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606429"
---
# <a name="storport-io-model-overview"></a>Storport i/o 模型概述

本部分介绍 Storport 驱动程序的 i/o 模型，并将此模型与 SCSI 端口驱动程序的模型进行比较。 Storport i/o 模型包含多个功能，旨在充分利用高速总线和存储设备的性能潜能。

Storport 驱动程序使用 i/o 的推送模式。 这意味着，驱动程序会将 i/o 请求异步转发到其微型端口驱动程序，直到达到最大数量的重叠数据包，而无需等待微型端口驱动程序请求输入。 在推送模型中，端口驱动程序控制 i/o 请求的流动，并将请求推送到微型端口驱动程序。

另一方面，SCSI 端口驱动程序使用 i/o 的请求模型。 在 i/o 的请求模型中，SCSI 端口驱动程序会以同步方式将 i/o 请求转发到其微型端口驱动程序，并等待微型端口驱动程序在发送下一个 i/o 请求之前请求新输入。 此外，微型端口驱动程序控制 i/o 请求的流，并从端口驱动程序中取出请求。

有关 SCSI 端口驱动程序的 i/o 模型的详细信息，请参阅[Scsi 端口 I/o 型号](scsi-port-i-o-model.md)。
