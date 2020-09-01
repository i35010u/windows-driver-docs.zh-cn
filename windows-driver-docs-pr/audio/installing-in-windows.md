---
title: 在 Windows 中安装
description: 在 Windows 中安装
ms.assetid: 790caffd-ebb0-4ba1-b31c-b03d3c83bc59
keywords:
- 音频适配器 WDK，系统组件
- 适配器驱动程序 WDK 音频，系统组件
- 端口类音频适配器 WDK，系统组件
ms.date: 10/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: f731477c1fb25de0ccb5cba368ed8c8993dc1338
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209089"
---
# <a name="installing-in-windows"></a>在 Windows 中安装


在以下 INF 设备驱动程序安装部分的示例中，这两个指令添加了用于在 Windows 中安装音频适配器核心系统组件的系统驱动程序信息：

```inf
  [XYZ-Audio-Device.Registration.NTX86]
  Include=ks.inf, wdmaudio.inf
  Needs=KS.Registration, WDMAUDIO.Registration
```

有关 **Include** 和 **需求** 指令的信息，请参阅 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md)。

 

