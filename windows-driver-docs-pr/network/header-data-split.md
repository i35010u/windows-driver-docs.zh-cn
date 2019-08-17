---
title: 标头-数据拆分简介
description: 标头-数据拆分简介
ms.assetid: ecbf4b08-8be4-42ca-8a65-1cb8124bee33
keywords:
- 标头-数据拆分 WDK
- 将标头和数据拆分为单独的缓冲区
- 缓冲区 WDK 标头-数据拆分
- 接收数据 WDK 网络
- 帧 WDK 标头-数据拆分
- 拆分框架 WDK 标头-数据拆分
- 存储 WDK 标头-数据拆分
- space 管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0bbe6a27bbf26d2bb40bb0022423e3e7f4088e1
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565681"
---
# <a name="introduction-to-header-data-split"></a>标头-数据拆分简介

本部分介绍在 NDIS 6.1 和更高版本中可用的标头数据拆分服务。 *标头-数据拆分*通过将接收的以太网帧中的标头和数据拆分为单独的缓冲区来改善网络性能。 分隔标头和数据可使标头一起收集到更小的内存区域中。 因此, 一个内存页中将容纳更多的标头, 并且系统缓存中将容纳更多的标头, 因此降低了驱动程序堆栈中内存访问的开销。

本部分包括：

[标头数据拆分概述](header-data-split-overview.md)

[初始化标头-数据拆分提供程序](initializing-a-header-data-split-provider.md)

[拆分以太网帧](splitting-ethernet-frames.md)

[接收标头-数据拆分的指示](receive-indications-with-header-data-split.md)

[标头-数据拆分管理和配置](header-data-split-administration-and-configuration.md)

[支持标头-协议驱动程序和筛选器驱动程序中的数据拆分](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)

 

 





