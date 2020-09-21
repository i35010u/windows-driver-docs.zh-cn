---
title: 标头数据拆分简介
description: 标头数据拆分简介
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
ms.openlocfilehash: eba8d6ed7e25ed24e10edc4447df19723053caa7
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90811974"
---
# <a name="introduction-to-header-data-split"></a>标头数据拆分简介

本部分介绍在 NDIS 6.1 和更高版本中可用的标头数据拆分服务。 *标头-数据拆分* 通过将接收的以太网帧中的标头和数据拆分为单独的缓冲区来改善网络性能。 分隔标头和数据可使标头一起收集到更小的内存区域中。 因此，一个内存页中将容纳更多的标头，并且系统缓存中将容纳更多的标头，因此降低了驱动程序堆栈中内存访问的开销。

本节包括：

[标头数据拆分概述](header-data-split-architecture.md)

[初始化标头数据拆分提供程序](initializing-a-header-data-split-provider.md)

[拆分以太网帧](splitting-ethernet-frames.md)

[标头数据拆分的接收指示](receive-indications-with-header-data-split.md)

[标头数据拆分管理和配置](setting-the-current-header-data-split-configuration.md)

[在协议驱动程序和筛选器驱动程序中支持标头数据拆分](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)

 

 





