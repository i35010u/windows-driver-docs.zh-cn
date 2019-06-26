---
title: 确定设备的父设备
description: 确定设备的父设备
ms.assetid: 61458911-222f-46aa-bc0e-a61ee25337bb
keywords:
- 安装程序 Api 函数 WDK，确定父项
- 父设备确定 WDK SetupAPI
- 设备父级 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c255879083ca9d700c37a58da149646799823ff5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374243"
---
# <a name="determining-the-parent-of-a-device"></a>确定设备的父设备





有时有必要访问设备的父级。 例如，某些类型的硬件设备的操作取决于特定父和子设备组之间的固定关系。 若要卸载此类硬件设备，则必须卸载所有子设备以及父。 若要卸载父级，你必须获取[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)父结构。 通用串行总线 (USB) 的复合设备，例如，多功能打印机，是此类设备。 表示在系统中的父级的复合设备和一个或多个子接口设备 (请参阅[USB 驱动程序堆栈体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index))。 若要卸载多功能打印机，必须卸载其父级的复合设备包括其所有子接口设备。

当插) 设备对设备树。 用于确定设备的父级的方法取决于如何配置该设备当前在系统中，按如下所示：

-   如果设备具有 devnode 设备树中，使用[ **CM_Get_Parent** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)若要获取其父级的设备实例句柄。 给定设备实例句柄，可以获取[设备实例 ID](device-instance-ids.md)和一个[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)结构的设备。 有关详细信息，请参阅[获取的设备在设备树中父](obtaining-the-parent-of-a-device-in-the-device-tree.md)。

-   如果设备已随其父级一起固定的关系，您可以保存和检索其父级的设备实例 ID。 当设备变为虚幻时，可以使用其设备实例句柄来获取设备的 SP_DEVINFO_DATA 结构。 有关详细信息，请参阅[确定的父级的 Nonpresent 设备](determining-the-parent-of-a-nonpresent-device.md)。

 

 





