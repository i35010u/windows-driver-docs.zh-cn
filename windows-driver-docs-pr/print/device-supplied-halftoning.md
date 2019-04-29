---
title: 设备提供的半色调
description: 设备提供的半色调
ms.assetid: d1d7963e-c23e-4cb5-a33f-43fec5dc74d2
keywords:
- 设备提供半色调 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a539326bb9879a6c56baba893e5f4daa16e14ef0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387272"
---
# <a name="device-supplied-halftoning"></a>设备提供的半色调





如果您的打印机在内部提供半色调功能，你的微型驱动程序必须指定，Unidrv 向打印机发送激活这些功能的命令。 对于每个半色调选项是打印机支持 GPD 文件的半色调\*功能条目必须包含\*，如下所示命令的每个设备提供半色调选项，条目：

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

此外必须指定 ColorMode 功能条目，并且它们必须包括\*DevBPP 和\*DevNumOfPlanes 条目描述打印机所需的输入的格式。

 

 




