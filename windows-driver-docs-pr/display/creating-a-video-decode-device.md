---
title: 创建视频解码设备
description: 创建视频解码设备
ms.assetid: a9820da9-436f-40b7-a25d-3208600f7a2f
keywords:
- 视频解码 WDK DirectX VA，创建解码设备
- 解码视频 WDK DirectX VA，创建解码设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40b7a1c45f920982d4bc9f34eba620d57e30bfb5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370231"
---
# <a name="creating-a-video-decode-device"></a>创建视频解码设备


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **CreateDecodeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice)函数来创建视频加速 (VA) 解码设备。 当与解码设备完成 Direct3D 运行时，它会调用用户模式显示驱动程序的[ **DestroyDecodeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroydecodedevice)函数。

 

 





