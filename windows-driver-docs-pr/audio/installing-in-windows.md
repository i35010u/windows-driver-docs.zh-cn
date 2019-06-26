---
title: 在 Windows 中安装
description: 在 Windows 中安装
ms.assetid: 790caffd-ebb0-4ba1-b31c-b03d3c83bc59
keywords:
- 音频适配器 WDK、 系统组件
- 适配器驱动程序 WDK 音频，系统组件
- 端口类音频适配器 WDK、 系统组件
ms.date: 10/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d74d0b559c939a3a23ee3ce097c6841fdfbc59c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359872"
---
# <a name="installing-in-windows"></a>在 Windows 中安装


INF 设备驱动程序安装部分的以下示例中，在两个指令添加将音频适配器的核心系统组件安装在 Windows 的系统驱动程序信息：

```inf
  [XYZ-Audio-Device.Registration.NTX86]
  Include=ks.inf, wdmaudio.inf
  Needs=KS.Registration, WDMAUDIO.Registration
```

璝惠**Include**并**需要**指令，请参阅[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)。

 

 




