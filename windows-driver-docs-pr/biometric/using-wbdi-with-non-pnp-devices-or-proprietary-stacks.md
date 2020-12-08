---
title: 将 WBDI 用于非 PnP 设备或专有堆栈
description: 将 WBDI 用于非 PnP 设备或专有堆栈
keywords:
- 生物识别驱动程序 WDK，旧版
- 生物识别驱动程序 WDK，非 PnP 设备
- 生物识别驱动程序 WDK，专用堆栈
- 旧驱动程序堆栈 WDK 生物识别
- 非 PnP 设备 WDK 生物识别
- 专用堆栈生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7876e5e6c8fb6aca4a0e08d5f2ecaaa651c84ede
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784263"
---
# <a name="using-wbdi-with-non-pnp-devices-or-proprietary-stacks"></a>将 WBDI 用于非 PnP 设备或专有堆栈


WBDI 不支持非 PnP 设备。 但是，非 PnP 生物识别设备和使用非 WBDI 驱动程序堆栈的设备仍可以与 WBDI 进行交互。

使用 WBDI 的旧驱动程序堆栈有两种主要方法：

1.  创建新的传感器插件来管理生物识别读卡器到达和出发。

2.  在检测生物识别功能或事件的现有设备堆栈上安装总线筛选器。 然后，总线筛选器会为 WBDI 驱动程序创建一个 PDO。

创建筛选器以管理 WBDI PDOs 是两个解决方案中的更简单的方法，这是 Microsoft 建议的方法。

 

 





