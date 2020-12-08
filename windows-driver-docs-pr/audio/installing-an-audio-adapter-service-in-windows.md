---
title: 安装音频适配器服务
description: 安装音频适配器服务
keywords:
- 音频适配器 WDK，服务安装
- 适配器驱动程序 WDK 音频，服务安装
- 端口类音频适配器 WDK，服务安装
- 适配器服务 WDK 音频
ms.date: 10/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a1faf3244cc565f404cbe52e0cc8b9ca6311749
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784741"
---
# <a name="installing-an-audio-adapter-service-in-windows"></a>在 Windows 中安装音频适配器服务

以下 [**INF AddService 指令**](../install/inf-addservice-directive.md) 将为 XYZ 音频设备安装适配器驱动程序 Xyzaud.sys：

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

 

