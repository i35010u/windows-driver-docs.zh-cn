---
title: 关于 LSI_U3 设备的示例 Storport 微型端口驱动程序
description: LSI_U3 设备的示例 Storport 微型端口驱动程序
ms.assetid: 1ac63d07-f85c-492b-9886-f40a19d7c0b2
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: d53a0ce35f9bfcb698198b6430cb81d16c9f893c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184925"
---
# <a name="about-the-sample-storport-miniport-driver-for-an-lsi_u3-device"></a>关于 LSI_U3 设备的示例 Storport 微型端口驱动程序

[LSI_U3 storport 微型端口驱动程序示例](/samples/microsoft/windows-driver-samples/lsi_u3-storport-miniport-driver/
)是在移植到使用 Storport 而不是 Scsiport 时，LSI SYM_U3 的基于 Scsiport 的小型端口驱动程序。 生成的基于 Storport 的微型端口驱动程序支持具有 53C1010-33 或 53C1010-66 芯片的 LSI Ultra160 并行 SCSI 主机总线适配器。 这些主机总线适配器的一些特征包括：

- 具有最小智能的较旧技术 SCSI 控制器硬件

- 具有 8 KB 内部 RAM 的非常简单的自定义8位 RISC 处理器

- 每个适配器限制为使用256队列标记值的硬件和脚本

- 用于匹配 Scsiport 功能的硬件和脚本

在 LSI_U3 微型端口驱动程序中进行了调整，以便将 Storport 高级功能与主机总线适配器本身的有限硬件功能相匹配。