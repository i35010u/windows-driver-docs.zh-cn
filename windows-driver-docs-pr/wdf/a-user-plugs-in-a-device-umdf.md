---
title: 用户插入设备
description: 用户插入设备
ms.assetid: 1968270b-ce57-4a8c-8b7a-bbd4a972435d
keywords:
- 电源管理方案 WDK UMDF，插入设备
- 插入设备方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64c5ccdaa14cdee12c6250133683dc0ba1b79745
ms.sourcegitcommit: c6040377fd6dd99031e4085a60ffbab4e1052dc2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84421380"
---
# <a name="a-user-plugs-in-a-device"></a>用户插入设备


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当用户插入设备时，框架会按以下顺序调用 UMDF 驱动程序的 PnP 和电源管理回拨方法，从图底部的设备到达状态开始：

![umdf 驱动程序的设备枚举和启动顺序](images/umdf-powerup-sequence.png)

框架首先调用驱动程序的[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调，以便驱动程序可以创建设备回调对象，并使用框架设备对象来表示设备。 此框架通过在整个序列中向上遍历来继续调用驱动程序的回调例程，直到设备正常运行。

对于每次支持设备的每个 UMDF 函数或筛选器驱动程序，框架都会继续执行此序列，每次使用驱动程序堆栈中最低的驱动程序。

 



