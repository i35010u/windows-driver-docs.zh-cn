---
title: 照相机的驱动程序的照相机类 INF 文件设置
description: 介绍如何将照相机类设置添加到通用的照相机的驱动程序 INF 文件。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb833199746b0367efef8dfa2edba9177859f303
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387938"
---
# <a name="camera-class-inf-file-setting-for-universal-camera-drivers"></a>通用相机驱动程序的相机类 INF 文件设置

从 Windows 10 版本 1709，应将以下照相机类设置添加到你通用照相机的驱动程序 INF 文件。

添加以下**类**并**ClassGuid**条目**版本**通用照相机驱动程序 INF 文件以确保您的驱动程序的部分将通过将来照相机驱动程序 HLK 测试：

```INF
[Version]

...

Class=Camera
ClassGuid={ca3e7ab9-b4c3-4ae6-8251-579ef933890f}

...
```

照相机类 INF 文件设置的 HLK 要求的详细信息，请参阅**Device.Streaming.Camera.Base.AVStreamClassInterfaceAndWDM**元件和外设的文档中[Windows适用于 Windows 10 的硬件兼容性规范](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)。
