---
title: LSI_U3 设备的示例 Storport 微型端口驱动程序
description: LSI_U3 设备的示例 Storport 微型端口驱动程序
ms.assetid: 1ac63d07-f85c-492b-9886-f40a19d7c0b2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a76fd738869e78f5aad6e72a55b0fb000dcd68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520842"
---
# <a name="sample-storport-miniport-driver-for-an-lsiu3-device"></a>LSI 示例 Storport 微型端口驱动程序\_U3 设备


LSI\_U3 Storport 微型端口驱动程序示例代码包含在 WDK 中是 LSI 的生产符号\_后要进行迁移，可使用而不是 Scsiport Storport 基于 U3 Scsiport 的微型端口驱动程序。 生成的基于 Storport 微型端口驱动程序支持 LSI Ultra160 并行 SCSI 主机总线适配器与 53 C 1010 33 或 53 C 1010 66 芯片上。 这些主机总线适配器的特征包括：

-   较旧的技术使用最小智能的 SCSI 控制器硬件

-   非常简单的自定义 8 位 RISC 处理器 8 KB 内部 ram

-   硬件和限制为使用每个适配器的 256 个队列标记值的脚本

-   硬件和脚本来匹配 Scsiport 功能

LSI 中进行了调整\_U3 微型端口驱动程序以匹配 Storport 对的高级功能有限的硬件功能的主机总线适配器本身。

 

 




