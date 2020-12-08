---
title: 从 BGR8888 转换为 XR_BIAS
description: 从 BGR8888 转换为 XR_BIAS
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，将 BGR8888 转换为 XR_BIAS
- 扩展格式 WDK Windows 7 显示，将 BGR8888 转换为 XR_BIAS
- 将 BGR8888 转换为 XR_BIAS WDK Windows 7 显示器
- BGR8888 WDK Windows 7 显示
- BGR8888 WDK Windows 7 显示，转换到 XR_BIAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52f9e7306e153d19957b5c1b7c013865c8ea6e9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810119"
---
# <a name="conversion-from-bgr8888-to-xr_bias"></a>从 BGR8888 到 XR 偏向的转换 \_


本部分仅适用于 Windows 7 及更高版本的操作系统。

从 BGR8888 格式转换 (例如，DXGI \_ FORMAT \_ B8G8R8A8 \_ UNORM) 为 \_ 无损。

缩放比例510显式选择为在 BGR8888 类型格式和 XR 偏差之间提供完全可逆的转换， \_ 而不会导致缩放系数为511的0.5 附近的非线性跳跃。

 

 





