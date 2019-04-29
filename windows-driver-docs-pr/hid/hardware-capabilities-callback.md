---
title: 硬件功能回调
description: 硬件功能回调
ms.assetid: 407505e4-c0d7-4e12-80d7-55801a66f531
keywords:
- 回调 WDK 游戏杆
- 游戏杆 WDK HID，功能
- 硬件功能回调 WDK 游戏杆
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 537057e18b0a1a297b5f57bce263b20173486a42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388935"
---
# <a name="hardware-capabilities-callback"></a>硬件功能回调





```cpp
int __stdcall HWCapsRoutine( int joyid, LPJOYOEMHWCAPS pjhwc );
```

每当请求设备的硬件功能，称为 HWCapsRoutine。 具体而言，VJoyD 调用 HWCapsRoutine 之前它将返回从 VJOYD\_注册\_设备\_驱动程序。 因此，很重要的驱动程序完成的情况下，此调用依赖之前注册该设备的任何初始化。 这些值通常是常量。 设备具有四个按钮和三个轴，其中第三个可能会返回被限制或方向舵值，下面是相应：

```cpp
pjhwc->dwMaxButtons = 4;    /* This should always be the number of buttons */
pjhwc->dwMaxAxes = 4;       /* The largest axis number which may be requested */
pjhwc->dwNumAxes = 3;       /* The number of axes the device has */
```

 

 




