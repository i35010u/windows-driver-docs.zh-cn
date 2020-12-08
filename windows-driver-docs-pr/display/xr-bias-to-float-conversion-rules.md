---
title: XR_BIAS 到浮点数转换规则
description: XR_BIAS 到浮点数转换规则
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，将 XR_BIAS 转换为 float
- 扩展格式 WDK Windows 7 显示，将 XR_BIAS 转换为 float
- 将 XR_BIAS 转换为浮动 WDK Windows 7 显示
- XR_BIAS WDK Windows 7 显示
- XR_BIAS WDK Windows 7 显示，转换为 float
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dc5b17018e6a493ff5df48f56f24b86e5acf8c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805611"
---
# <a name="xr_bias-to-float-conversion-rules"></a>XR \_ 偏移转换规则


本部分仅适用于 Windows 7 及更高版本的操作系统。

下面的代码演示如何将 XR \_ 偏移转换为 float：

```cpp
float XRtoFloat( UINT XRComponent ) {
// The & 0x3ff shows that only 10 bits contribute to the conversion. 
 return (float)( (XRComponent & 0x3ff) - 0x180 ) / 510.f;
}
```

 

 





