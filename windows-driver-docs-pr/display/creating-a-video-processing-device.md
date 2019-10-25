---
title: 创建视频处理设备
description: 创建视频处理设备
ms.assetid: 3bedf0bf-360a-4dad-a7dd-ee73a0f1fc31
keywords:
- 视频处理 WDK DirectX VA，创建设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f649f90d8d93ee143e763ad4c73f4fcfa5658e17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839776"
---
# <a name="creating-a-video-processing-device"></a>创建视频处理设备


Microsoft Direct3D runtime 调用用户模式显示驱动程序的[**CreateVideoProcessDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createvideoprocessdevice)函数来创建用于处理视频流的设备。 当 Direct3D 运行时完成设备后，它将调用用户模式显示驱动程序的[**DestroyVideoProcessDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyvideoprocessdevice)函数。

 

 





