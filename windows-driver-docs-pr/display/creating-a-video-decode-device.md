---
title: 创建视频解码设备
description: 创建视频解码设备
ms.assetid: a9820da9-436f-40b7-a25d-3208600f7a2f
keywords:
- 视频解码 WDK DirectX VA，创建解码设备
- 解码视频 WDK DirectX VA，创建解码设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f9c90a41208008edae57dc7c072ccb8f696ed1b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066052"
---
# <a name="creating-a-video-decode-device"></a>创建视频解码设备


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**CreateDecodeDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice) 函数来创建用于视频加速 (VA) 的解码设备。 当 Direct3D 运行时完成解码设备后，它将调用用户模式显示驱动程序的 [**DestroyDecodeDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroydecodedevice) 函数。

 

