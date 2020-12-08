---
title: 设备提供的半色调
description: 设备提供的半色调
keywords:
- 设备提供的半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb39efc20e8d3ed039779d7a180b0b56a53f8e3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797237"
---
# <a name="device-supplied-halftoning"></a>设备提供的半色调





如果打印机在内部提供半色调功能，则微型驱动程序必须指定 Unidrv 发送到打印机以激活这些功能的命令。 对于支持打印机的每个半色调选项，GPD 文件的半色调 \* 功能条目必须包含 \* 每个设备提供的半色调选项的命令条目，如下所示：

```cpp
*Feature: Halftone
{
    *Option: CustomHalftoneMethod1
    {
        *Name: "Custom Halftone Method 1"
        *Command: CmdSelect: "<printer command string>"
    }
    *Option: CustomHalftoneMethod2
    {
        *Name: "Custom Halftone Method 2"
        *Command: CmdSelect: "<printer command string>"
    }
}
```

还必须指定 ColorMode 功能条目，并且它们必须包含 \* \* 描述打印机所需输入格式的 DevBPP 和 DevNumOfPlanes 条目。

 

 




