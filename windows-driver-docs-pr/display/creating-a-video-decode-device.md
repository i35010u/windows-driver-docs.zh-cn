---
title: 创建视频解码设备
description: 创建视频解码设备
keywords:
- 视频解码 WDK DirectX VA，创建解码设备
- 解码视频 WDK DirectX VA，创建解码设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e236596d6e86700adaedfb4c1914ce34fd9e2866
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834607"
---
# <a name="creating-a-video-decode-device"></a>创建视频解码设备


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**CreateDecodeDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice) 函数来创建用于视频加速 (VA) 的解码设备。 当 Direct3D 运行时完成解码设备后，它将调用用户模式显示驱动程序的 [**DestroyDecodeDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroydecodedevice) 函数。

 

