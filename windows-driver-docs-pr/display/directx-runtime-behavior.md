---
title: DirectX 运行时行为
description: DirectX 运行时行为
ms.assetid: 98cfb09c-74ed-4329-b663-5f813a84debe
keywords:
- DirectX 运行时旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 372583ec4dba115e3a086f43a8d259ecc442cca0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533011"
---
# <a name="directx-runtime-behavior"></a>DirectX 运行时行为


各种版本的 Microsoft DirectX 运行时处理以下旋转代表该驱动程序的情况下：

-   Microsoft DirectDraw 运行时将自动失败时将显示旋转显示覆盖层的任何尝试。

-   所有版本的 DirectX 运行时都调整主图面，以便扫描行值涵盖整个范围最多的解决方法的高度旋转时返回的扫描行值。 否则，尝试自己想追踪的应用程序可能停止响应等待扫描行值的最大的显示宽度，并在应用程序将否则永远不会在纵向模式下。

-   所有版本的 DirectX 运行时都处理到旋转主面上的所有访问都是通过使用各种形式的仿真窗口模式设备来建立。

 

 





