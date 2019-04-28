---
title: ControllerControl 例程的存储要求
description: ControllerControl 例程的存储要求
ms.assetid: 1ee69144-5f52-4d61-ad30-02e8fbe1f91e
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程编写
- ControllerControl 例程存储
- 存储 WDK 控制器对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5f855379f2fd0eb9e5474aaf545c72807610ace
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331959"
---
# <a name="storage-requirements-for-controllercontrol-routines"></a>ControllerControl 例程的存储要求





如果它具有*ControllerControl*例程，非 WDM 驱动程序必须提供适用于驻留存储*ControllerObject*返回指针[ **IoCreateController**](https://msdn.microsoft.com/library/windows/hardware/ff548395).

驱动程序可以提供必要的存储设备扩展在或中由驱动程序分配的非分页缓冲池。 通常情况下，使用控制器对象的驱动程序存储*ControllerObject*在每个设备对象，表示受由控制器的硬件的物理或逻辑设备的设备扩展中的指针对象。

驱动程序编写器可以决定的大小和内部结构*ControllerObject*-&gt;**ControllerExtension**。

一个控制器对象，不能有一个名称，该对象不能为目标的 I/O 请求。 它通常表示的硬件控制一组同构的 I/O 请求的实际目标的设备。

 

 




