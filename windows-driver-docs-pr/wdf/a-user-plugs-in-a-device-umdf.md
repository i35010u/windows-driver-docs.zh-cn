---
title: '用户插入设备 (UMDF 1) '
description: 用户插入设备
keywords:
- 电源管理方案 WDK UMDF，插入设备
- 插入设备方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fd192a43eb15de8ecf27a13e9c0d1491dc60c5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837615"
---
# <a name="a-user-plugs-in-a-device-umdf-1"></a>用户插入设备 (UMDF 1) 


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当用户插入设备时，框架会按以下顺序调用 UMDF 驱动程序的 PnP 和电源管理回拨方法，从图底部的设备到达状态开始：

![umdf 驱动程序的设备枚举和启动顺序](images/umdf-powerup-sequence.png)

框架首先调用驱动程序的 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 回调，以便驱动程序可以创建设备回调对象，并使用框架设备对象来表示设备。 此框架通过在整个序列中向上遍历来继续调用驱动程序的回调例程，直到设备正常运行。

对于每次支持设备的每个 UMDF 函数或筛选器驱动程序，框架都会继续执行此序列，每次使用驱动程序堆栈中最低的驱动程序。

