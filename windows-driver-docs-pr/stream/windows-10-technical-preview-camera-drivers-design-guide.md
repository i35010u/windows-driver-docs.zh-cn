---
title: 适用于 Windows 10 的通用照相机驱动程序设计指南
description: 适用于 Windows 10 的照相机的驱动程序接口的所有设备聚合，并使用通用的照相机的驱动程序模型。
ms.assetid: CB5EEDF2-650D-4CD3-A5DE-DF0D6F10B394
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30be0220c48c29aff792afc99f7196dbba7ae793
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329943"
---
# <a name="universal-camera-driver-design-guide-for-windows-10"></a>适用于 Windows 10 的通用照相机驱动程序设计指南


适用于 Windows 10 的照相机的驱动程序接口的所有设备聚合，并使用通用的照相机的驱动程序模型。

通用的照相机的驱动程序模型还包含新 DDIs，包括：

* [数字视频防抖](ksproperty-cameracontrol-extended-videostabilization.md)
* [可变帧速率](ksproperty-cameracontrol-extended-vfr.md)
* [人脸检测](ksproperty-cameracontrol-extended-facedetection.md)
* [视频高动态范围 (HDR)](ksproperty-cameracontrol-extended-videohdr.md)
* [光学防抖](ksproperty-cameracontrol-extended-ois.md)
* [场景分析：照片 HDR、闪光、无闪光、超微光](ksproperty-cameracontrol-extended-advancedphoto.md)
* [捕获统计信息：元数据框架/属性、直方图](ksproperty-cameracontrol-extended-histogram.md)
* [平滑缩放](ksproperty-cameracontrol-extended-zoom.md)
* [硬件优化提示](ksproperty-cameracontrol-extended-optimizationhint.md)
* [相机配置文件](ksproperty-cameracontrol-extended-profile.md)

## <a name="build-a-universal-camera-driver"></a>生成通用照相机驱动程序

通用照相机驱动程序是基于 AVStream 微型驱动程序[Windows 驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff565698)(WDM)。

有关详细信息，请参阅以下各节中的[适用于 Windows 10 的通用照相机驱动程序模型参考](windows-10-technical-preview-camera-drivers-reference.md):

* [新的照相机的驱动程序控件](camera-driver-controls.md)
* [新摄像头驱动程序枚举](camera-driver-enumerations.md)
* [新的照相机的驱动程序函数](camera-driver-functions.md)
* [新的照相机的驱动程序结构](camera-driver-structures.md)

有关生成 AVStream 微型驱动程序的详细信息，请参阅以下主题：

* [AVStream 概述](avstream-overview.md)
* [编写 AVStream 微型驱动程序](writing-an-avstream-minidriver.md)



