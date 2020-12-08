---
title: 示例扩展单元描述符
description: 示例扩展单元描述符
keywords:
- 扩展单元描述符 WDK USB 视频类
- 描述符 WDK USB 视频类
- 描述符 WDK USB 视频类，示例代码
- 示例代码 WDK USB 视频类，扩展单元描述符
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 932bae5399d37e5211e6d1fdbf4b530a644c421d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804347"
---
# <a name="sample-extension-unit-descriptor"></a>示例扩展单元描述符

此代码演示如何在硬件级别提供扩展单元说明符。

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

有关 USB 视频类硬件要求的详细信息，请参阅 *Video DevicesSpecification 的通用串行总线设备类定义*。 此规范可在 [USB 实现论坛](https://www.usb.org/) 网站上找到。
