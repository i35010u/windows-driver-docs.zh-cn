---
title: 创建视频处理设备
description: 创建视频处理设备
keywords:
- 视频处理 WDK DirectX VA，创建设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae86e1c36b812da5a8e066f15bb3a9b3fe62842d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834603"
---
# <a name="creating-a-video-processing-device"></a>创建视频处理设备


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**CreateVideoProcessDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createvideoprocessdevice) 函数来创建用于处理视频流的设备。 当 Direct3D 运行时完成设备后，它将调用用户模式显示驱动程序的 [**DestroyVideoProcessDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyvideoprocessdevice) 函数。

 

