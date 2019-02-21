---
title: 卸载设备和驱动程序包
description: 卸载设备和驱动程序包
ms.assetid: 4381ee42-778b-402d-b242-892ec921c28f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d35ac477ef83ca28c2a23b5b4adaeb90e54af305
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544221"
---
# <a name="uninstalling-devices-and-driver-packages"></a>卸载设备和驱动程序包


安装设备后，可能需要卸载设备或[驱动程序包](driver-packages.md)。 例如，最终用户可能会决定将为关联的设备，或可能需要更新驱动程序后，卸载该驱动程序包。

当您卸载设备时，必须删除设备节点 (*devnode*)，表示系统中的设备的物理实例。

当您卸载[驱动程序包](driver-packages.md)，必须完成以下操作：

-   删除与之关联的文件[驱动程序包](driver-packages.md)从[驱动程序存储区](driver-store.md)。

-   删除驱动程序包的二进制文件。

本部分介绍如何卸载设备和驱动程序包。 这被专为驱动程序开发人员想要向其客户提供说明或工具。

本部分包括以下主题：

[如何卸载设备和驱动程序包](how-devices-and-driver-packages-are-uninstalled.md)

[使用设备管理器卸载设备和驱动程序包](using-device-manager-to-uninstall-devices-and-driver-packages.md)

[使用 SetupAPI 卸载设备和驱动程序包](using-setupapi-to-uninstall-devices-and-driver-packages.md)



