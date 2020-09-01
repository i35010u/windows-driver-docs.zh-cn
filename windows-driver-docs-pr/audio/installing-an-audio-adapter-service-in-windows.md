---
title: 安装音频适配器服务
description: 安装音频适配器服务
ms.assetid: 465005da-bf06-497b-801c-fe5aa19a3974
keywords:
- 音频适配器 WDK，服务安装
- 适配器驱动程序 WDK 音频，服务安装
- 端口类音频适配器 WDK，服务安装
- 适配器服务 WDK 音频
ms.date: 10/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a2b9269b695a5af41ad502878921f577b92cb87
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209437"
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

 

