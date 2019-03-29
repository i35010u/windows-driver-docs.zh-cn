---
title: 创建视频处理设备
description: 创建视频处理设备
ms.assetid: 3bedf0bf-360a-4dad-a7dd-ee73a0f1fc31
keywords:
- 视频处理 WDK DirectX VA，创建设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbccc35674a7f1531d321facaee55e6c93502976
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575452"
---
# <a name="creating-a-video-processing-device"></a>创建视频处理设备


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **CreateVideoProcessDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540729)函数来创建用于处理视频流的设备。 当与设备完成 Direct3D 运行时，它会调用用户模式显示驱动程序的[ **DestroyVideoProcessDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552814)函数。

 

 





