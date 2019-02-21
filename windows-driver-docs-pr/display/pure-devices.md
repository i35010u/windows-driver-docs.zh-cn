---
title: 纯设备
description: 纯设备
ms.assetid: 6ad3412c-fd80-41c0-9abc-117aacc5ddae
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，纯设备
- 纯设备 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dad6e90c59628d677f3ddc45d3dc4978fc04aecc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543935"
---
# <a name="pure-devices"></a>纯设备


## <span id="ddk_pure_devices_gg"></span><span id="DDK_PURE_DEVICES_GG"></span>


DirectX 8.0 引入了"纯"设备的概念。 使用纯设备时，运行时不跟踪状态或状态块或执行代表硬件处理任何软件顶点。 此外，应用程序无法查询后的从运行时状态。 缺少状态跟踪，尤其是状态块正在使用时，可能会导致应用程序的显著的性能提升。

硬件直接支持的唯一顶点处理可供该应用程序时使用的是纯的设备。 例如，对于不支持硬件转换和照明的卡，仅 pretransformed 的顶点可以传递到 Direct3D。 此外，API 函数**SetClipStatus**， **GetClipStatus**并**ProcessVertices**不能用于纯设备。

若要使用纯设备应用程序必须请求它与设备创建标记 D3DCREATE\_PUREDEVICE 和驱动程序必须报告其充当纯设备的能力。

 

 





