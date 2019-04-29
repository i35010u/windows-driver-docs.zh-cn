---
title: 从 BGR8888 转换为 XR_BIAS
description: 从 BGR8888 转换为 XR_BIAS
ms.assetid: 53145cfe-d344-4242-b124-ddb507d876ad
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，将 BGR8888 转换为 XR_BIAS
- 扩展的格式 WDK Windows 7 显示，将 BGR8888 转换为 XR_BIAS
- 将 BGR8888 转换为 XR_BIAS WDK Windows 7 显示
- BGR8888 WDK Windows 7 显示
- BGR8888 WDK Windows 7 显示，转换为 XR_BIAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9acd50bbd2bc5e56628e27d3f529f039fff17e73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368631"
---
# <a name="conversion-from-bgr8888-to-xrbias"></a>从 BGR8888 转换为 XR\_偏差


本部分仅适用于 Windows 7 和更高版本的操作系统。

从 BGR8888 类型格式的转换 (例如，DXGI\_格式\_B8G8R8A8\_UNORM) 到 XR\_偏移是无损。

510 的比例因子显式选择提供 BGR8888 类型格式和 XR 之间的完全可逆转转换\_偏置没有导致附近 0.5 的非线性跳转将隐含 511 的比例因子。

 

 





