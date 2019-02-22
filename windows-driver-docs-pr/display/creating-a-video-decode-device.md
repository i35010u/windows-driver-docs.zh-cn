---
title: 创建视频解码设备
description: 创建视频解码设备
ms.assetid: a9820da9-436f-40b7-a25d-3208600f7a2f
keywords:
- 视频解码 WDK DirectX VA，创建解码设备
- 解码视频 WDK DirectX VA，创建解码设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36d730edde511cf927c786959c9d1062def722f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523680"
---
# <a name="creating-a-video-decode-device"></a>创建视频解码设备


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **CreateDecodeDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540618)函数来创建视频加速 (VA) 解码设备。 当与解码设备完成 Direct3D 运行时，它会调用用户模式显示驱动程序的[ **DestroyDecodeDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552757)函数。

 

 





