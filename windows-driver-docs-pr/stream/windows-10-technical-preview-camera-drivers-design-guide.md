---
title: 适用于 Windows 10 的通用照相机驱动程序设计指南
description: 适用于 Windows 10 的照相机的驱动程序接口的所有设备聚合，并使用通用的照相机的驱动程序模型。
ms.assetid: CB5EEDF2-650D-4CD3-A5DE-DF0D6F10B394
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fc8ef50d7469cbe7ca6d9cf62424e88def4d18b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385356"
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

通用照相机驱动程序是基于 AVStream 微型驱动程序[Windows 驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)(WDM)。

有关详细信息，请参阅以下各节中的[适用于 Windows 10 的通用照相机驱动程序模型参考](windows-10-technical-preview-camera-drivers-reference.md):

* [新的照相机的驱动程序控件](camera-driver-controls.md)
* [新摄像头驱动程序枚举](camera-driver-enumerations.md)
* [新的照相机的驱动程序函数](camera-driver-functions.md)
* [新的照相机的驱动程序结构](camera-driver-structures.md)

有关生成 AVStream 微型驱动程序的详细信息，请参阅以下主题：

* [AVStream 概述](avstream-overview.md)
* [编写 AVStream 微型驱动程序](writing-an-avstream-minidriver.md)



