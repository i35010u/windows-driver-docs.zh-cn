---
title: XR_BIAS 浮动的转换规则
description: XR_BIAS 浮动的转换规则
ms.assetid: fef4a1cb-6567-4d8f-aa8a-ceed00eefec8
keywords:
- 转换 XR_BIAS 浮动的 Direct3D 版本 10.1 WDK Windows 7 显示
- 扩展的格式 WDK Windows 7 显示，转换 XR_BIAS 浮动
- 将 XR_BIAS 转换为 float WDK Windows 7 显示
- XR_BIAS WDK Windows 7 显示
- XR_BIAS WDK Windows 7 显示、 转换为浮点型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebaf3c24d26207973755fe44d1d5d512d118203b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521749"
---
# <a name="xrbias-to-float-conversion-rules"></a>XR\_偏置浮动的转换规则


本部分仅适用于 Windows 7 和更高版本的操作系统。

下面的代码演示如何将转换 XR\_为浮点型偏差：

```cpp
float XRtoFloat( UINT XRComponent ) {
// The & 0x3ff shows that only 10 bits contribute to the conversion. 
 return (float)( (XRComponent & 0x3ff) - 0x180 ) / 510.f;
}
```

 

 





