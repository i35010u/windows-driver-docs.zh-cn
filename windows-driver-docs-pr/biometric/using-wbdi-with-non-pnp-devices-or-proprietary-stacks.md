---
title: 将 WBDI 用于非 PnP 设备或专有堆栈
description: 将 WBDI 用于非 PnP 设备或专有堆栈
ms.assetid: 0143eae4-4ca8-4b25-9a97-2cace74f8de9
keywords:
- 生物识别驱动程序 WDK，旧
- 生物识别驱动程序 WDK，非 PnP 设备
- 生物识别驱动程序 WDK、 专有堆栈
- 旧驱动程序堆栈 WDK 生物识别
- 非 PnP 设备 WDK 生物识别
- 专有堆栈 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3103760af97d510a505a5119e5bc2b0fc3439ec6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575252"
---
# <a name="using-wbdi-with-non-pnp-devices-or-proprietary-stacks"></a>将 WBDI 用于非 PnP 设备或专有堆栈


WBDI 不支持非 PnP 设备。 但是，非 PnP 生物识别设备和使用非 WBDI 驱动程序堆栈的设备仍可通过使用 WBDI 中。

有两种主要方法使用 WBDI 旧驱动程序堆栈：

1.  创建新的传感器插件来管理生物识别读取器到达和离开的。

2.  在检测到生物识别功能或事件的现有设备堆栈上安装总线筛选器。 然后，总线筛选器创建 WBDI 驱动程序的 PDO。

创建一个筛选器来管理 WBDI PDOs 较简单的两个解决方案，这是 Microsoft 推荐的方法。

 

 





