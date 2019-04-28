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
ms.openlocfilehash: 86f81e2b9a783d30193dc83b271bfaf74eec515f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333454"
---
# <a name="installing-in-windows"></a>在 Windows 中安装


INF 设备驱动程序安装部分的以下示例中，在两个指令添加将音频适配器的核心系统组件安装在 Windows 的系统驱动程序信息：

```inf
  [XYZ-Audio-Device.Registration.NTX86]
  Include=ks.inf, wdmaudio.inf
  Needs=KS.Registration, WDMAUDIO.Registration
```

璝惠**Include**并**需要**指令，请参阅[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)。

 

 




