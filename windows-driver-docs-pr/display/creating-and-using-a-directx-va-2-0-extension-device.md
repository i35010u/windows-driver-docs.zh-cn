---
title: 创建和使用 DirectX VA 2.0 扩展设备
description: 创建和使用 DirectX VA 2.0 扩展设备
ms.assetid: 650a77a5-67c3-4b11-93c8-24232905eb43
keywords:
- DirectX 视频加速 WDK 显示，扩展支持
- 视频加速 WDK DirectX，扩展支持
- VA WDK DirectX，扩展支持
- 扩展设备 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a1547c9016d02e3bba756d0cc12a29ae07b455a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370203"
---
# <a name="creating-and-using-a-directx-va-20-extension-device"></a>创建和使用 DirectX VA 2.0 扩展设备


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **CreateExtensionDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createextensiondevice)函数为 DirectX VA 2.0 创建扩展设备。 当与设备完成 Direct3D 运行时，它会调用用户模式显示驱动程序的[ **DestroyExtensionDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyextensiondevice)函数。

Direct3D 运行时将调用用户模式显示驱动程序[ **DecodeExtensionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute)函数进行解码的非标准的视频解码设备之间的帧开始和结束帧时间段以及上特定的呈现目标图面。 解码视频有关的一般讨论，请参阅[视频解码](decoding-video.md)。

Direct3D 运行时将调用用户模式显示驱动程序[ **ExtensionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_extensionexecute)函数来执行使用了非标准扩展设备上的 DirectX VA 2.0 操作。

 

 





