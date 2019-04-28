---
title: 创建视频处理设备
description: 创建视频处理设备
ms.assetid: 3bedf0bf-360a-4dad-a7dd-ee73a0f1fc31
keywords:
- 视频处理 WDK DirectX VA，创建设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbccc35674a7f1531d321facaee55e6c93502976
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346923"
---
# <a name="creating-a-video-processing-device"></a>创建视频处理设备


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **CreateVideoProcessDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540729)函数来创建用于处理视频流的设备。 当与设备完成 Direct3D 运行时，它会调用用户模式显示驱动程序的[ **DestroyVideoProcessDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552814)函数。

 

 





