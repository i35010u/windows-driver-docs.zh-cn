---
title: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树
description: HKLM\SYSTEM\CurrentControlSet\Enum 注册表树包含系统上的设备的相关信息。
ms.assetid: 9de3ca54-d23f-4ee6-a638-27e52a60dfdd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b247b445248e624a98f7377b95a5a26d95a19f54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386412"
---
# <a name="hklmsystemcurrentcontrolsetenum-registry-tree"></a>HKLM\\系统\\CurrentControlSet\\枚举注册表树





**HKLM\\系统\\CurrentControlSet\\枚举**注册表树包含系统上的设备的相关信息。 PnP 管理器中的窗体的名称创建一个用于每个设备的子项**HKLM\\系统\\CurrentControlSet\\枚举\\** <em>枚举器</em> **\\** <em>deviceID</em>。 在每个项是一个用于每个系统上存在的设备实例的子项。 此子项具有设备描述、 硬件 Id、 兼容 Id 和资源要求等信息。

**枚举**树保留供操作系统组件，其布局会有所更改。 驱动程序和用户模式下[设备安装组件](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))必须使用系统提供的函数，如[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)和[ **SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)，以从该树中提取信息。 *驱动程序和 Windows 应用程序不能访问****枚举****直接树。* 您可以查看**枚举**直接通过调试驱动程序时使用注册表编辑器的树。

 

 





