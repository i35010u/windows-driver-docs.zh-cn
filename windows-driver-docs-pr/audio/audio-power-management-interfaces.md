---
title: 音频电源管理界面
description: 音频电源管理界面
ms.assetid: 7b123d3f-4f11-448e-8b20-92578fda7e69
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65b4bcef0a0e841ac22fbc71df774139e1289534
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355660"
---
# <a name="audio-power-management-interfaces"></a>音频电源管理界面


## <span id="ddk_audio_power_management_interfaces_ks"></span><span id="DDK_AUDIO_POWER_MANAGEMENT_INTERFACES_KS"></span>


本部分中描述的接口端口 Class Library (portcls.sys) 用来管理 WDM 音频适配器中的能力。 这些接口由适配器驱动程序实现，并公开给 PortCls 系统驱动程序。

讨论了以下两个接口：

由适配器驱动程序实现和公开给 PortCls 的音频的适配器的电源管理的。

由适配器驱动程序实现和公开给 PortCls。 此接口提供了有关音频适配器和系统的电源管理消息。

如果需要提前通知即将发生的电源状态更改的微型端口驱动程序可以公开一个可选接口。

[IAdapterPowerManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement)

[IAdapterPowermanagement2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement2)

[IAdapterPowerManagement3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement3)

[IPowerNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-ipowernotify)

 

 





