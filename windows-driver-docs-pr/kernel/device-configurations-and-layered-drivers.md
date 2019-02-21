---
title: 设备配置和分层驱动程序
description: 对于最常见类型的设备，Windows Driver Kit (WDK) 提供了完全正常运行的系统驱动程序的一组示例。
ms.assetid: 1baaac5a-8eea-42df-bad6-fe620ac32a6c
keywords:
- WDM 驱动程序 WDK 内核配置
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 将驱动程序
- 可重复使用的驱动程序 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d0ce221816c0507c1143737287e478bfd11078e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533134"
---
# <a name="device-configurations-and-layered-drivers"></a>设备配置和分层驱动程序


对于最常见类型的设备，Windows Driver Kit (WDK) 提供了完全正常运行的系统驱动程序的一组示例。 各个示例驱动程序可以用作模型，开发新的驱动程序的相似类型的设备时。 但是，系统的驱动程序有一个额外的设计要求： 若要轻松地开发新的设备驱动程序。 因此，有许多系统的驱动程序的分层式体系结构，以便可以重复使用某些驱动程序以支持新的驱动程序的类似的设备。




在大多数情况下，WDK 提供可重复使用驱动程序是 WDM 驱动程序支持即插即用和处理系统提供特定于设备的最低级别 （即插即用总线） 驱动程序的独立于硬件的操作。 在某些情况下，例如并行端口和 SCSI 端口驱动程序，这些可重复使用的驱动程序为更高级别的、 特定于设备的类型的类驱动程序提供支持。 请注意无系统的可重用的驱动程序可以阻止新的中间驱动程序添加到现有的驱动程序的链的开发。

新 （或替换） 驱动程序的设备驱动程序链中的适当位置部分取决于在给定的 Windows 平台，和部分多少支持新的驱动程序可以从现有系统驱动程序获取设备的硬件配置。

## <a name="in-this-section"></a>本部分内容


-   [示例设备和驱动程序配置](sample-device-and-driver-configuration.md)
-   [添加驱动程序时考虑的要点](points-to-consider-when-adding-drivers.md)

 

 




