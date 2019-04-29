---
title: 示例扩展单元描述符
description: 示例扩展单元描述符
ms.assetid: 283a28e6-9f73-4131-bcfb-b4983a92cecd
keywords:
- 扩展单元描述符 WDK USB 视频类
- 描述符 WDK USB 视频类
- 描述符 WDK USB 视频类，示例代码
- 示例代码 WDK USB 视频类扩展单元描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e48e469e0016179d1be1e05f2bc08f4daa7edc0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389211"
---
# <a name="sample-extension-unit-descriptor"></a>示例扩展单元描述符


此代码演示如何提供在硬件级别的扩展单元描述符。

```cpp
BYTE  Length:            0x1a    
BYTE  DescriptorType:    0x24               
BYTE  DescriptorSubtype: 0x06             
BYTE  bUnitID:           0x05
GUID  guidExtensionCode: xxxxxxxx-xxxx-xxxx-xxxxxxxxxxxxxxxx
BYTE  bNumControls:      0x03
BYTE  bNrInPins:         0x01
BYTE  baSourceID[0]:     0x01
```

有关详细的 USB 视频类的硬件要求的信息，请参阅*通用串行总线的设备类定义视频 DevicesSpecification*。 此规范位于[USB 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)网站。

 

 




