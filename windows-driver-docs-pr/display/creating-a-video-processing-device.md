---
title: 创建视频处理设备
description: 创建视频处理设备
ms.assetid: 3bedf0bf-360a-4dad-a7dd-ee73a0f1fc31
keywords:
- 视频处理 WDK DirectX VA，创建设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d7ca4ae86f624ebba7734a6b88781c62e890c30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370225"
---
# <a name="creating-a-video-processing-device"></a>创建视频处理设备


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **CreateVideoProcessDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createvideoprocessdevice)函数来创建用于处理视频流的设备。 当与设备完成 Direct3D 运行时，它会调用用户模式显示驱动程序的[ **DestroyVideoProcessDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyvideoprocessdevice)函数。

 

 





