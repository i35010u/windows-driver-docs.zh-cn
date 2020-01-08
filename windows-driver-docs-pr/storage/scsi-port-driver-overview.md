---
title: SCSI 端口驱动程序概述
description: SCSI 端口驱动程序概述
ms.assetid: e97ea5f2-7f20-4d3d-82a2-7d83e1eba30e
keywords:
- 存储端口驱动程序 WDK，SCSI 端口驱动程序
- SCSI 端口驱动程序 WDK 存储
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 61aaac571d5d8b06466f2001716903d2804cf3fa
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606501"
---
# <a name="scsi-port-driver-overview"></a>SCSI 端口驱动程序概述

Microsoft 将 SCSI 端口驱动程序作为 Microsoft Windows 存储体系结构的一项标准功能提供。 SCSI 端口驱动程序通过模拟简化的 SCSI 适配器来简化 Windows 存储子系统。 存储类驱动程序加载到端口驱动程序的顶层。 这意味着，你可以编写适用于 Windows 的存储类驱动程序，只需对每个 SCSI 适配器的独特硬件功能进行考虑。

SCSI 端口驱动程序的模拟功能还允许开发比单一端口驱动程序更简单的设计和代码的微型驱动程序。 换而言之，使用 SCSI 端口驱动程序可以专注于开发用于处理适配器的特定功能的微型端口驱动程序。

若要使用 SCSI 端口支持例程，请链接到某个 SCSI 端口支持库*scsiport*或*scsiwmi*。 这些 SCSI 端口库处理小型端口驱动程序与操作系统的硬件抽象层（HAL）之间的所有交互。 微型端口驱动程序不得直接链接到 HAL 支持库、 *hal*，也不应直接链接到*ntoskrnl.exe*或*libcntpr*支持库。 这样做的 SCSI 微型端口驱动程序不符合 Windows 徽标的要求。

以下各节检查 SCSI 端口驱动程序的主要功能。

- [SCSI 端口提供的功能](capabilities-provided-by-scsi-port.md)

- [SCSI 端口驱动程序支持例程](scsi-port-driver-support-routines.md)

- [带有存储类驱动程序的 SCSI 端口接口](scsi-port-s-srb-interface-with-the-storage-class-driver.md)

- [SCSI 端口具有 SCSI 端口微型端口驱动程序的接口](scsi-port-s-interface-with-scsi-port-miniport-drivers.md)

- [SCSI 端口 i/o 模型](scsi-port-i-o-model.md)

Scsi 端口微型驱动程序的一般讨论在[Scsi 微型端口驱动程序](scsi-miniport-drivers.md)中提供。

Windows 存储体系结构还提供了[Storport 驱动程序](storport-driver-overview.md)，这是用于高性能设备的 SCSI 端口的建议替代方法。
