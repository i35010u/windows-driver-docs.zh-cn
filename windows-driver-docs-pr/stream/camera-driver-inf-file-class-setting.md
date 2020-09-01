---
title: 照相机驱动程序的照相机类 INF 文件设置
description: 描述如何将 "照相机类" 设置添加到通用照相机驱动程序 INF 文件中。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 155d348ef4a2964f542ae127e7c5028fe109e88c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185409"
---
# <a name="camera-class-inf-file-setting-for-universal-camera-drivers"></a>通用相机驱动程序的相机类 INF 文件设置

从 Windows 10 版本1709开始，你应该向通用照相机驱动程序 INF 文件添加以下相机类设置。

将这些 " **类** " 和 " **ClassGuid** " 条目添加到通用照相机驱动程序 INF 文件的 " **版本** " 部分，以确保驱动程序可以通过未来的照相机驱动程序的 HLK 测试：

```INF
[Version]

...

Class=Camera
ClassGuid={ca3e7ab9-b4c3-4ae6-8251-579ef933890f}

...
```

有关 "照相机类 INF 文件" 设置的 HLK 要求的详细信息，请参阅[适用于 windows 10 的 Windows 硬件兼容性规范](/windows-hardware/design/compatibility/whcp-specifications-policies)的 "组件和外设" 文档中的**AVStreamClassInterfaceAndWDM** 。