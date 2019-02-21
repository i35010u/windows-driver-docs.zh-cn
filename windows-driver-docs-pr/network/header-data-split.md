---
title: 标头数据拆分
description: 标头数据拆分
ms.assetid: ecbf4b08-8be4-42ca-8a65-1cb8124bee33
keywords:
- 标头数据拆分 WDK
- 拆分标头和数据，以单独的缓冲区
- 缓冲区 WDK 标头数据拆分
- 接收数据 WDK 网络
- 帧 WDK 标头数据拆分
- 拆分帧 WDK 标头数据拆分
- 存储 WDK 标头数据拆分
- 空间管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4097ae3ab00bdf04ed2addff44b895bf9de31a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534045"
---
# <a name="header-data-split"></a>标头数据拆分





本部分介绍标头数据拆分 NDIS 6.1 和更高版本中可用的服务。 *标头数据拆分*可以提高网络性能，通过将标头和接收到的以太网帧中的数据拆分为单独的缓冲区。 分离的标头和数据可以在要收集的内存较小的区域放入标头。 因此，多个标头可放入单个内存页和多个标头将显示系统缓存中，因此驱动程序堆栈中的内存访问开销已降低。

本部分包括：

[标头数据拆分概述](header-data-split-overview.md)

[初始化标头数据拆分提供程序](initializing-a-header-data-split-provider.md)

[拆分以太网帧](splitting-ethernet-frames.md)

[接收指示标头数据拆分](receive-indications-with-header-data-split.md)

[标头数据拆分管理和配置](header-data-split-administration-and-configuration.md)

[支持协议驱动程序和筛选器驱动程序中的标头数据拆分](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)

 

 





