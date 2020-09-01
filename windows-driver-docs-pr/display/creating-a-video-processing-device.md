---
title: 创建视频处理设备
description: 创建视频处理设备
ms.assetid: 3bedf0bf-360a-4dad-a7dd-ee73a0f1fc31
keywords:
- 视频处理 WDK DirectX VA，创建设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc6b6738b1f8e577afc0915de347d013e058e72a
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064864"
---
# <a name="creating-a-video-processing-device"></a>创建视频处理设备


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**CreateVideoProcessDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createvideoprocessdevice) 函数来创建用于处理视频流的设备。 当 Direct3D 运行时完成设备后，它将调用用户模式显示驱动程序的 [**DestroyVideoProcessDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyvideoprocessdevice) 函数。

 

