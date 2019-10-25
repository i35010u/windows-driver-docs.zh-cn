---
title: 创建视频解码设备
description: 创建视频解码设备
ms.assetid: a9820da9-436f-40b7-a25d-3208600f7a2f
keywords:
- 视频解码 WDK DirectX VA，创建解码设备
- 解码视频 WDK DirectX VA，创建解码设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56659ae8a0e7ceb25d047aed98c0089ca9ae6fc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839778"
---
# <a name="creating-a-video-decode-device"></a>创建视频解码设备


Microsoft Direct3D runtime 调用用户模式显示驱动程序的[**CreateDecodeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice)函数来创建视频加速（VA）的解码设备。 当 Direct3D 运行时完成解码设备后，它将调用用户模式显示驱动程序的[**DestroyDecodeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroydecodedevice)函数。

 

 





