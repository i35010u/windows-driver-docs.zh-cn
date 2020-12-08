---
title: 卸载设备和驱动程序包
description: 卸载设备和驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 309f4e66c6be275a24b3bbd7635814f20ca5c607
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804107"
---
# <a name="uninstalling-devices-and-driver-packages"></a>卸载设备和驱动程序包


设备安装完成后，可能需要卸载设备或 [驱动程序包](driver-packages.md)。 例如，最终用户可能决定替换关联的设备，或者在更新驱动程序时可能必须卸载驱动程序包。

卸载设备时，必须删除设备节点 (*devnode*) ，该设备表示系统中设备的物理实例。

卸载 [驱动程序包](driver-packages.md)时，必须完成以下操作：

-   从[驱动程序存储区](driver-store.md)中删除与[驱动程序包](driver-packages.md)关联的文件。

-   删除驱动程序包的二进制文件。

本部分介绍如何卸载设备和驱动程序包。 它适用于想要向客户提供说明或工具的驱动程序开发人员。

本节包括下列主题：

[如何卸载设备和驱动程序包](how-devices-and-driver-packages-are-uninstalled.md)

[使用设备管理器卸载设备和驱动程序包](using-device-manager-to-uninstall-devices-and-driver-packages.md)

[使用 SetupAPI 卸载设备和驱动程序包](using-setupapi-to-uninstall-devices-and-driver-packages.md)



