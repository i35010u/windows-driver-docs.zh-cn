---
title: 填充 ESRT 表
description: EFI 系统资源表 (ESRT) 提供了一种机制，用于标识集成设备和系统固件资源，以使固件更新面向这些资源。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24e11738710045856c75043965083b8ca9df5479
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784187"
---
# <a name="populating-the-esrt-table"></a>填充 ESRT 表


EFI 系统资源表 (ESRT) 提供了一种机制，用于标识集成设备和系统固件资源，以使固件更新面向这些资源。 ESRT 中的每个条目描述了可供固件更新驱动程序包使用的设备或系统固件资源。 固件更新驱动程序包可更新的每个固件资源必须只由 ESRT 中的一个条目描述，以便能够部署和安装固件更新。 有关 ESRT 的布局和实现的更多详细信息，请参阅 [ESRT 表定义](esrt-table-definition.md)。

下图显示了典型 SoC 系统的概要框图。

![soc 系统上的可更新固件](images/updatablefirmwareonsoc.png)

在此示例中，包含可更新固件的每个系统设备均由单个块表示。 每个块都能接收和安装设备的目标独立固件更新。 因此，每个块在表示该设备的 ESRT 中都有唯一的条目，如下图所示。

![soc 系统固件资源](images/socfirmwareresources.png)

设备还可以将其固件更新为单一单一单一系统固件更新驱动程序包的一部分。 在这种情况下，设备不会有 ESRT 条目，因为使用系统固件更新了它。 通常，设备只能将其固件更新作为 ESRT 中的一个条目的目标。

为简单起见，上图描述了一个模型，其中每个设备的固件更新以唯一的条目为目标。 表中的每个 GUID 标识了可更新的设备或此 SoC 系统内的 UEFI 系统固件。 表中的每个 GUID 都是唯一的 (也就是说，没有两个设备/系统固件共享同一 GUID 值) 并且该表对于单个 SoC 系统是唯一的。 SoC 系统的硬件修订必须为设备/系统固件定义新的 GUID 值。 这可确保固件不再到修改后的硬件中的每个组件，因为在不同版本中设备硬件的细微差异可能需要不同的固件。

## <a name="related-topics"></a>相关主题
[通过固件驱动程序包进行的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[自定义不同地理区域的固件](customizing-firmware-for-different-geographic-regions.md)  
[创作固件更新包](authoring-a-firmware-update-package.md)  
[认证和签署更新包](certifying-and-signing-the-update-package.md)  
[安装更新](installing-the-update.md)  



