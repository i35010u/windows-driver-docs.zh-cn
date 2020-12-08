---
title: 定义 "64 位" 字段的方法1
description: 为驱动程序定义 "64 位" 字段
keywords:
- 32位 i/o 支持 WDK 64 位，已定义64位字段
- 64位字段定义的 WDK 内核
- 位域 WDK 64 位
- 分离控制代码 WDK 64 位
- 控制代码 WDK 64 位
- 文件系统控制代码 WDK 64 位
- FSCTL WDK 64 位
- I/o 控制代码 WDK 内核，64位驱动程序中的32位 i/o
- IOCTLs WDK 内核，64位驱动程序中的32位 i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 130345f03591e5934c7430d9e7833d6495d09c47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788583"
---
# <a name="technique-1-defining-a-64bit-field"></a>方法1：定义 "64 位" 字段





"64 位" 字段是在 IOCTL 或 FSCTL 控件代码中定义的。 此字段包含一个位标志，该标志始终设置为64位调用方，但对于32位，始终为 clear。 将控制代码中的哪个位选为 "64 位" 字段是特定于驱动程序的，但它必须是从未为32位调用方设置的位。 大多数驱动程序的一个不错的选择是函数字段中 (MSB) 最有效的位。

例如，32位驱动程序中使用的 IOCTL (FSCTL) 控制代码包含四个位域：

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
<td><p>2位</p></td>
<td><p>12位</p></td>
<td><p>2位</p></td>
</tr>
</tbody>
</table>

 

只要没有现有的驱动程序定义的控制代码在函数字段中设置 MSB，这些控制代码就可以继续由32位用户模式应用程序使用。

为了容纳64位调用方，驱动程序将定义一个长度较短的函数字段。 此位重定义为 "64 位" 字段：

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
<th>64</th>
<th>函数</th>
<th>方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>16 位</p></td>
<td><p>2位</p></td>
<td><p>1位</p></td>
<td><p>11 位</p></td>
<td><p>2位</p></td>
</tr>
</tbody>
</table>

 

下面的代码示例演示如何在驱动程序头文件中定义 "64 位" 字段：

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

 

 




