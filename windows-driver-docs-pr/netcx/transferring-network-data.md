---
title: NetAdapterCx 数据路径简介
description: NetAdapterCx 数据路径简介
ms.assetid: D2AC8269-F2D5-4FDC-A59E-6A35DBB18FF0
keywords:
- NetAdapterCx 传输网络数据，NetCx 传输网络数据
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a1468c06e8f3fb4436f905b7813de9abb024965f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208959"
---
# <a name="introduction-to-the-netadaptercx-data-path"></a>NetAdapterCx 数据路径简介

若要观看介绍 NetAdapterCx 中的数据路径模型的视频，请参阅第9频道上的[网络适配器类扩展：数据路径](https://aka.ms/netadapter/video3)视频。

在 NetAdapterCx 模型中，网络数据由数据包描述符表示，并通过数据包队列传输。 OS 和客户端驱动程序使用一组与每个数据包队列关联的环形缓冲区将数据包描述符相互传输。

以下主题详细说明了如何在 NetAdapterCx 客户端驱动程序中传输网络数据。

- [数据包描述符和扩展](packet-descriptors-and-extensions.md)
- [传输和接收队列](transmit-and-receive-queues.md)
- [净环简介](introduction-to-net-rings.md)
- [网络数据缓冲区管理](network-data-buffer-management.md)
