---
title: 用于 ProcAmp 控制的反交错容器设备
description: 用于 ProcAmp 控制的反交错容器设备
keywords:
- 容器设备 WDK DirectX VA
- 取消隔行扫描 WDK DirectX VA，ProcAmp control
- ProcAmp WDK DirectX VA，取消隔行扫描容器设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a47dc0270d2c685a330d12f22d5c9452f8c3f05
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809593"
---
# <a name="deinterlace-container-device-for-procamp-control"></a>用于 ProcAmp 控制的反交错容器设备


## <span id="ddk_deinterlace_container_device_for_procamp_control_gg"></span><span id="DDK_DEINTERLACE_CONTAINER_DEVICE_FOR_PROCAMP_CONTROL_GG"></span>


[ProcAmp 控件的示例函数](sample-functions-for-procamp-control.md)只能在 DirectX VA 设备的上下文中使用，因此必须首先定义和创建隔行扫描容器设备。

如果驱动程序支持 ProcAmp 控件调整) ，则用于 [取消隔行扫描的隔行扫描容器设备](deinterlace-container-device-for-deinterlacing.md) 还可用于 ProcAmp 控件，以确定 ProcAmp 控制 (设备的功能。 如果支持，驱动程序将在 VMR 启动调用时创建 ProcAmp 控件设备。

**注意**   取消隔行扫描容器设备只是一种软件构造，不代表设备上包含的任何功能硬件。

 

 

 





