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
ms.openlocfilehash: b90c70565ee9992607398f8fcc10923ee03fdd96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358116"
---
# <a name="wakefromd0-wakefromd1-wakefromd2-and-wakefromd3"></a>WakeFromD0、WakeFromD1、WakeFromD2 和 WakeFromD3





每种[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构成员指示设备是否可以被唤醒以响应到达时在设备处于指定状态的外部信号。

支持所有四个设备电源的设备状态 D0、 D1、 D2 （D3） 但可仅从状态 D0 和 D1，唤醒**WakeFromD0**并**WakeFromD1**位将设置，和**WakeFromD2**并**WakeFromD3**位都被清除。

 

 




