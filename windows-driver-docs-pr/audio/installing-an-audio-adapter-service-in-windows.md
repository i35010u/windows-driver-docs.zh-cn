---
title: 安装的音频适配器服务
description: 安装的音频适配器服务
ms.assetid: 465005da-bf06-497b-801c-fe5aa19a3974
keywords:
- 音频适配器 WDK，服务安装
- 适配器驱动程序 WDK 音频，服务安装
- 端口类音频适配器 WDK，服务安装
- 适配器服务 WDK 音频
ms.date: 10/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69fab800bc97d16bc70d0579eb365d802547e367
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359894"
---
# <a name="installing-an-audio-adapter-service-in-windows"></a>在 Windows 中安装音频适配器服务

以下[ **INF AddService 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)的 XYZ 音频设备安装适配器驱动程序 Xyzaud.sys:

```cpp
  [XYZ-Audio-Device.Services.NTX86]
  AddService = XYZ-Audio-Device, 0x00000002, XYZ-Audio-Device.Service.Install

  [XYZ-Audio-Device.Service.Install]
  DisplayName   = %XYZ-Audio-Device.ServiceDescription%
  ServiceType   = 1                  ; SERVICE_KERNEL_DRIVER
  StartType     = 3                  ; SERVICE_DEMAND_START
  ErrorControl  = 1                  ; SERVICE_ERROR_NORMAL
  ServiceBinary = %12%\system32\drivers\xyzaud.sys
```

 

 




