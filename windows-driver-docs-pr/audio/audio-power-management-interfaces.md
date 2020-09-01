---
title: 音频电源管理界面
description: 音频电源管理界面
ms.assetid: 7b123d3f-4f11-448e-8b20-92578fda7e69
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98962eb26df438e537634759a9d22e8b2a10af24
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208291"
---
# <a name="audio-power-management-interfaces"></a>音频电源管理界面


## <span id="ddk_audio_power_management_interfaces_ks"></span><span id="DDK_AUDIO_POWER_MANAGEMENT_INTERFACES_KS"></span>


本部分介绍端口类库 ( # A0) 用于管理 WDM 音频适配器中电源的接口。 这些接口由适配器驱动程序实现并公开给 PortCls 系统驱动程序。

讨论以下两个接口：

由适配器驱动程序实现并向 PortCls 显示，用于音频适配器卡的电源管理。

由适配器驱动程序实现并向 PortCls 公开。 此接口提供有关音频适配器和系统的电源管理消息。

当微型端口驱动程序需要提前通知即将出现电源状态更改时可以公开的可选接口。

[IAdapterPowerManagement](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement)

[IAdapterPowermanagement2](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement2)

[IAdapterPowerManagement3](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement3)

[IPowerNotify](/windows-hardware/drivers/ddi/portcls/nn-portcls-ipowernotify)

 

