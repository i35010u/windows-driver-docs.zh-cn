---
title: 方法 1 定义"64 位"字段
description: 为驱动程序定义"64 位"字段
ms.assetid: 6498e66c-145e-4f7e-a065-cbd781e142cc
keywords:
- 32 位 I/O 支持 WDK 64 位、 64 位字段定义
- 64 位域定义 WDK 内核
- 位域 WDK 64 位
- 单独的控件代码 WDK 64 位
- 控制代码 WDK 64 位
- 文件系统控制代码 WDK 64 位
- FSCTL WDK 64 位
- I/O 控制代码 WDK 内核，在 64 位驱动程序中的 32 位 I/O
- Ioctl WDK 内核，在 64 位驱动程序中的 32 位 I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cd78bd2a9304cd6cfe3732189fc00828d43b17f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345537"
---
# <a name="technique-1-defining-a-64bit-field"></a>方法 1：定义一个"64 位"字段





IOCTL 或 FSCTL 控件代码中定义了"64 位"字段。 此字段包含的位标志始终设置为 64 位的调用方，但始终清除对 32 位。 选择哪一段中的控制代码，因为"64 位"字段是特定于驱动程序，但它必须是为 32 位的调用方永远不会设置的位。 适合于大多数驱动程序是函数字段中的最高有效位 (MSB)。

例如，在 32 位驱动程序中使用的 IOCTL (FSCTL) 控制代码包含四个位域：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>设备类型</th>
<th>访问</th>
<th>函数</th>
<th>方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>16 位</p></td>
<td><p>2 位</p></td>
<td><p>12 位</p></td>
<td><p>2 位</p></td>
</tr>
</tbody>
</table>

 

只要没有任何现有的驱动程序定义的控制代码设置 MSB 函数字段中，这些控制代码可以继续使用 32 位用户模式应用程序。

为了适应 64 位的调用方，驱动程序定义一个函数字段，是一位较短。 此位将重新定义为"64 位"字段：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>设备类型</th>
<th>访问</th>
<th>64Bit</th>
<th>函数</th>
<th>方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>16 位</p></td>
<td><p>2 位</p></td>
<td><p>1 的位</p></td>
<td><p>11 位</p></td>
<td><p>2 位</p></td>
</tr>
</tbody>
</table>

 

下面的代码示例演示如何在驱动程序标头文件中定义的"64 位"字段：

```cpp
#define REGISTER_FUNCTION 0     // Define the IOCTL function code

#ifdef  _WIN64
#define CLIENT_64BIT   0x800
#define REGISTER_FUNCTION 0
#define IOCTL_REGISTER   CTL_CODE(FILE_DEVICE_UNKNOWN, \
  CLIENT_64BIT|REGISTER_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
#else
#define IOCTL_REGISTER   CTL_CODE(FILE_DEVICE_UNKNOWN, \
  REGISTER_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
#endif

typedef struct _IOCTL_PARAMETERS {
    PVOID   Addr;
    SIZE_T  Length;
    HANDLE  Handle;
} IOCTL_PARAMETERS, *PIOCTL_PARAMETERS;
```

 

 




