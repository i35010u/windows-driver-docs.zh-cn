---
title: 单纯设备
description: 单纯设备
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，纯设备
- 纯设备 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be64588e0ecf8312b1676505f19705ea47e1d650
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838481"
---
# <a name="pure-devices"></a>单纯设备


## <span id="ddk_pure_devices_gg"></span><span id="DDK_PURE_DEVICES_GG"></span>


DirectX 8.0 引入了 "纯" 设备的概念。 使用纯设备时，运行时不会跟踪状态或状态块，也不会代表硬件执行任何软件顶点处理。 此外，应用程序无法从运行时查询回状态。 缺少状态跟踪，尤其是在使用状态块时，可能会导致应用程序的性能大幅提高。

使用纯设备时，应用程序只可使用硬件直接支持的顶点处理。 例如，对于不支持硬件转换和照明的卡，只能将 pretransformed 顶点传递到 Direct3D。 而且，API 函数 **SetClipStatus**、 **GetClipStatus** 和 **ProcessVertices** 不能与纯设备一起使用。

若要使用纯设备，应用程序必须使用设备创建标志来请求它 D3DCREATE \_ PUREDEVICE，驱动程序必须报告其充当纯设备的能力。

 

 





