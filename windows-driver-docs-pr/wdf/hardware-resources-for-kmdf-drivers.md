---
title: 处理硬件资源
description: 系统的硬件资源是 I/O 端口、 中断向量、 直接内存访问 (DMA) 通道和其他必须分配给每个设备都连接到系统的通信路径。
ms.assetid: 30ceb7db-f11e-498c-a0c0-a63218627c6e
keywords:
- 即插即用 WDK KMDF，硬件资源
- 插 WDK KMDF，硬件资源
- 硬件资源 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1565d982c3d4904b3d2227e8a6ef79dd6eb20d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391877"
---
# <a name="handling-hardware-resources"></a>处理硬件资源


系统的硬件资源是 I/O 端口、 中断向量、 直接内存访问 (DMA) 通道和其他必须分配给每个设备都连接到系统的通信路径。 在本部分中的主题介绍如何内核模式驱动程序框架 (KMDF) 驱动程序协商的设备的硬件资源要求，检查建议的资源的列表，然后接收和已分配的资源。 本部分还介绍了如何 KMDF 和用户模式驱动程序框架 (UMDF) 驱动程序访问和映射分配资源。




## <a name="in-this-section"></a>本节内容


-   [硬件资源简介](introduction-to-hardware-resources.md)
-   [硬件资源的 framework 对象](framework-objects-for-hardware-resources.md)
-   [创建资源的要求列表](creating-a-resource-requirements-list.md)
-   [修改资源要求列表](modifying-a-resource-requirements-list.md)
-   [启动配置为创建的资源列表](creating-a-resource-list-for-a-boot-configuration.md)
-   [修改资源的列表](modifying-a-resource-list.md)
-   [原始和已翻译资源](raw-and-translated-resources.md)
-   [查找和映射硬件资源](finding-and-mapping-hardware-resources.md)
-   [读取和写入设备注册](reading-and-writing-to-device-registers.md)

 

 





