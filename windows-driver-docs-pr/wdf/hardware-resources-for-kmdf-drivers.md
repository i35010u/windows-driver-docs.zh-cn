---
title: 处理硬件资源
description: 系统的硬件资源是 i/o 端口、中断向量、直接内存访问 (DMA) 通道，以及其他必须分配给连接到系统的设备的通信路径。
keywords:
- PnP WDK KMDF，硬件资源
- 即插即用 WDK KMDF，硬件资源
- 硬件资源 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a670fcc6255309712328bb636c26de4cfffdbe6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815616"
---
# <a name="handling-hardware-resources"></a>处理硬件资源


系统的硬件资源是 i/o 端口、中断向量、直接内存访问 (DMA) 通道，以及其他必须分配给连接到系统的设备的通信路径。 本节中的主题介绍 Kernel-Mode Driver Framework (KMDF) 驱动程序如何协调设备的硬件资源需求，查看建议的资源列表，然后接收分配的资源。 本部分还介绍了 KMDF 和 User-Mode Driver Framework 如何 (UMDF) 驱动程序访问和映射分配的资源。




## <a name="in-this-section"></a>在本节中


-   [硬件资源简介](introduction-to-hardware-resources.md)
-   [硬件资源的框架对象](framework-objects-for-hardware-resources.md)
-   [创建资源要求列表](creating-a-resource-requirements-list.md)
-   [修改资源要求列表](modifying-a-resource-requirements-list.md)
-   [为启动配置创建资源列表](creating-a-resource-list-for-a-boot-configuration.md)
-   [修改资源列表](modifying-a-resource-list.md)
-   [原始资源和已转换的资源](raw-and-translated-resources.md)
-   [查找和映射硬件资源](finding-and-mapping-hardware-resources.md)
-   [读取设备注册表和写入到设备注册表](reading-and-writing-to-device-registers.md)

 

 





