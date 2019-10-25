---
title: ControllerControl 例程的存储要求
description: ControllerControl 例程的存储要求
ms.assetid: 1ee69144-5f52-4d61-ad30-02e8fbe1f91e
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程，编写
- ControllerControl 例程，存储
- 存储 WDK 控制器对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eb446fb89b492040f49a6660d92ff274e6a824d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838404"
---
# <a name="storage-requirements-for-controllercontrol-routines"></a>ControllerControl 例程的存储要求





如果它具有*ControllerControl*例程，则非 WDM 驱动程序必须为[**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)返回的*ControllerObject*指针提供常驻存储。

驱动程序可以在设备扩展或驱动程序分配的非分页池中提供必要的存储。 通常，使用控制器对象的驱动程序将*ControllerObject*指针存储在代表由控制器对象表示的硬件控制的物理或逻辑设备的每个设备对象的设备扩展中。

驱动程序编写器确定*ControllerObject*-&gt;**ControllerExtension**的大小和内部结构。

不能为某个控制器对象指定一个名称，不能作为 i/o 请求的目标。 它表示的硬件通常控制一组同类设备，这些设备是 i/o 请求的实际目标。

 

 




