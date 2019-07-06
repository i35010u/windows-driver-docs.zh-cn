---
title: 简介 NetAdapterCx 数据路径
description: 简介 NetAdapterCx 数据路径
ms.assetid: D2AC8269-F2D5-4FDC-A59E-6A35DBB18FF0
keywords:
- 传输网络数据、 网络数据传输的 NetCx NetAdapterCx
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b78bafb63c16758a9efdc3f109520363d0eebe32
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608473"
---
# <a name="introduction-to-the-netadaptercx-data-path"></a>简介 NetAdapterCx 数据路径

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

若要观看的视频，引入了 NetAdapterCx 中的数据路径模型，请参阅[网络适配器类扩展：数据路径](https://aka.ms/netadapter/video3)第 9 频道上的视频。

在 NetAdapterCx 模型中，网络数据是由数据包描述符和通过数据包队列传输。 OS 和客户端驱动程序传输到使用环形缓冲区与每个数据包队列相关联的一组相互数据包描述符。

以下主题详细说明了如何将 NetAdapterCx 客户端驱动程序中的网络数据传输。

- [数据包描述符和扩展](packet-descriptors-and-extensions.md)
- [传输和接收队列](transmit-and-receive-queues.md)
- [网环和网环迭代器](net-rings-and-net-ring-iterators.md)
- [网络数据缓冲区管理](network-data-buffer-management.md)
