---
title: WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3
description: WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3
ms.assetid: f01aaceb-babf-42da-bc4b-1a846c84a313
keywords:
- WakeFromD0
- WakeFromD1
- WakeFromD2
- WakeFromD3
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9576c26d40775423cec5f382a9fb8d8c6e1ca8a8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193075"
---
# <a name="wakefromd0-wakefromd1-wakefromd2-and-wakefromd3"></a>WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3





其中每个 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities) 结构成员表示设备是否可以唤醒响应在设备处于指定状态时到达的外部信号。

对于支持所有四种设备电源状态 (D0，D1，D2，D3) 但只能从状态 D0 和 D1 进行唤醒的设备，将设置 **WakeFromD0** 和 **WakeFromD1** 位，并且 **WakeFromD2** 和 **WakeFromD3** 位清晰。

 

