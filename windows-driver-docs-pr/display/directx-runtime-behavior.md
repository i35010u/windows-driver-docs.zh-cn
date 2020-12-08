---
title: DirectX 运行时行为
description: DirectX 运行时行为
keywords:
- DirectX 运行时旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cf49d52fc7f92905fac01a66406ee93dcfff363
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809333"
---
# <a name="directx-runtime-behavior"></a>DirectX 运行时行为


各种版本的 Microsoft DirectX 运行时代表驱动程序处理下列循环情况：

-   Microsoft DirectDraw 运行时自动失败在显示旋转时任何显示覆盖的尝试。

-   所有版本的 DirectX 运行时都将调整主图面旋转时返回的扫描行值，以便扫描行值覆盖整个范围，直至达到分辨率的高度。 否则，如果尝试无线处理的应用程序等待的扫描行值大于显示器的宽度，而该应用程序在纵向模式下却从不接收，则该应用程序可能会停止响应。

-   所有版本的 DirectX 运行时都将处理对使用各种仿真模式的开窗模式设备发出的旋转的主表面的所有访问。

 

 





