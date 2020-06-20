---
title: 示例扩展单元描述符
description: 示例扩展单元描述符
ms.assetid: 283a28e6-9f73-4131-bcfb-b4983a92cecd
keywords:
- 扩展单元描述符 WDK USB 视频类
- 描述符 WDK USB 视频类
- 描述符 WDK USB 视频类，示例代码
- 示例代码 WDK USB 视频类，扩展单元描述符
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: f300d2ea5b06d1af006a7c06cb85e1de41d1e297
ms.sourcegitcommit: f29360d62eb77b6ee875ce66483d5bc72785eede
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85111245"
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

有关 USB 视频类硬件要求的详细信息，请参阅*Video DevicesSpecification 的通用串行总线设备类定义*。 此规范可在[USB 实现论坛](https://www.usb.org/)网站上找到。
