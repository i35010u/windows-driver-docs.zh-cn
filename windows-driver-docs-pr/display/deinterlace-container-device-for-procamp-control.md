---
title: 用于 ProcAmp 控制的反交错容器设备
description: 用于 ProcAmp 控制的反交错容器设备
ms.assetid: ce179efe-9e92-4407-8e90-896e4b9a2e84
keywords:
- 容器设备 WDK DirectX VA
- 取消隔行扫描 WDK DirectX va，因此 ProcAmp 控件
- ProcAmp WDK DirectX va，因此取消隔行扫描容器设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3357a55a9ca0edc9f24e89b44c28943a49eaca49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575292"
---
# <a name="deinterlace-container-device-for-procamp-control"></a>用于 ProcAmp 控制的反交错容器设备


## <span id="ddk_deinterlace_container_device_for_procamp_control_gg"></span><span id="DDK_DEINTERLACE_CONTAINER_DEVICE_FOR_PROCAMP_CONTROL_GG"></span>


[ProcAmp 控制的函数的示例](sample-functions-for-procamp-control.md)因此需要先定义并创建取消隔行扫描容器设备只可以 DirectX VA 设备上下文中使用。

[取消隔行扫描容器设备进行去隔行](deinterlace-container-device-for-deinterlacing.md)还可用 ProcAmp 控件来确定 ProcAmp 控制设备的功能 （如果该驱动程序支持 ProcAmp 控制调整）。 如果支持，驱动程序将创建 ProcAmp 控制设备，当 VMR 开始调用来执行此操作。

**请注意**  取消隔行扫描容器设备是软件构造并不表示任何包含的设备上起作用的硬件。

 

 

 





