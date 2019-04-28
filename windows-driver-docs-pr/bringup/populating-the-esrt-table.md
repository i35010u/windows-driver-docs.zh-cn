---
title: 填充 ESRT 表
description: EFI 系统资源表 (ESRT) 提供了一种机制，用于标识集成的设备和系统固件资源用于针对这些资源进行固件更新。
ms.assetid: 8C1FF785-7A05-4E10-9E38-C6AC597E3FA8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4070714be51d83082c8b6d6ad23ea2315c91f08e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337472"
---
# <a name="populating-the-esrt-table"></a>填充 ESRT 表


EFI 系统资源表 (ESRT) 提供了一种机制，用于标识集成的设备和系统固件资源用于针对这些资源进行固件更新。 ESRT 中的每个条目描述固件更新驱动程序包将作为目标的设备或系统固件资源。 可以更新固件更新驱动程序包的每个固件资源必须由某一项完全 ESRT 来启用固件更新部署和安装所述。 布局和 ESRT 实现的详细信息，请参阅[ESRT 表定义](esrt-table-definition.md)。

下图显示了典型的 SoC 系统的高级别块状图。

![soc 系统上的可更新固件](images/updatablefirmwareonsoc.png)

在此示例中，每个系统设备，包含可更新固件表示由单个块。 每个块都能够接收和安装设备的目标，而不管固件更新。 在这种情况下，每个块都有唯一条目中表示该设备，ESRT 以下关系图中所示。

![soc 系统固件资源](images/socfirmwareresources.png)

还有可能，使设备能够具有单一的整体系统固件更新驱动程序包的过程中更新其固件。 在这种情况下，设备将不有 ESRT 条目，因为它使用系统固件更新。 一般来说，设备只能 ESRT 的某一项针对其固件更新。

为简单起见上, 图介绍其中每台设备都与唯一项分别针对其固件更新的模型。 表中的每个 GUID 标识的可更新的设备或此 SoC 系统中的 UEFI 系统固件。 表中的每个 GUID 是唯一的 （即没有两个设备/系统固件共享相同的 GUID 值），表是唯一的单个 SoC 系统。 SoC 系统的硬件修订必须定义设备/系统固件的新 GUID 的值。 这可确保该固件是定目标到每个组件中的修改后的硬件，因为跨修订版本的设备硬件细微的差异可能需要不同的固件。

## <a name="related-topics"></a>相关主题
[通过固件驱动程序包的系统和设备固件更新](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[自定义不同的地理区域的固件](customizing-firmware-for-different-geographic-regions.md)  
[创作固件更新包](authoring-a-firmware-update-package.md)  
[认证和签名的更新包](certifying-and-signing-the-update-package.md)  
[安装更新](installing-the-update.md)  



