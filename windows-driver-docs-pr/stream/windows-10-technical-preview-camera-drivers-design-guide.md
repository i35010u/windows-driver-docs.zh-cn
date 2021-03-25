---
title: 适用于 Windows 10 的通用相机驱动程序设计指南
description: 适用于 Windows 10 的相机驱动程序接口已聚合到所有设备，并使用通用照相机驱动程序模型。
ms.date: 03/23/2021
ms.localizationpriority: medium
ms.openlocfilehash: b217bfc2eb2bd774809ecbb2639750a87773252b
ms.sourcegitcommit: 2a27786ed72024f064bbfef20933b0d0b429d4b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105106149"
---
# <a name="universal-camera-driver-design-guide-for-windows-10"></a>适用于 Windows 10 的通用相机驱动程序设计指南

适用于 Windows 10 的相机驱动程序接口已聚合到所有设备，并使用通用照相机驱动程序模型。

通用照相机驱动程序模型包含以下控件：

- [数字视频防抖](ksproperty-cameracontrol-extended-videostabilization.md)

- [可变帧速率](ksproperty-cameracontrol-extended-vfr.md)

- [人脸检测](ksproperty-cameracontrol-extended-facedetection.md)

- [视频高动态范围 (HDR)](ksproperty-cameracontrol-extended-videohdr.md)

- [光学防抖](ksproperty-cameracontrol-extended-ois.md)

- [场景分析：照片 HDR、闪光、无闪光、超微光](ksproperty-cameracontrol-extended-advancedphoto.md)

- [捕获统计信息：元数据框架/属性、直方图](ksproperty-cameracontrol-extended-histogram.md)

- [平滑缩放](ksproperty-cameracontrol-extended-zoom.md)

- [硬件优化提示](ksproperty-cameracontrol-extended-optimizationhint.md)

- [相机配置文件](ksproperty-cameracontrol-extended-profile.md)

## <a name="build-a-universal-camera-driver"></a>构建通用照相机驱动程序

通用照相机驱动程序是基于 [Windows 驱动模型](../kernel/introduction-to-wdm.md) (WDM) 构建的 AVStream 微型驱动程序。

有关详细信息，请参阅 [适用于 Windows 10 的通用照相机驱动程序参考](windows-10-technical-preview-camera-drivers-reference.md)中的以下部分：

- [适用于 Windows 10 的通用照相机驱动程序控件](camera-driver-controls.md)

- [适用于 Windows 10 的通用照相机驱动程序枚举](camera-driver-enumerations.md)

- [适用于 Windows 10 的通用照相机驱动程序功能](camera-driver-functions.md)

- [适用于 Windows 10 的通用照相机驱动程序结构](camera-driver-structures.md)

有关生成 AVStream 微型驱动程序的详细信息，请参阅以下主题：

- [AVStream 概述](avstream-overview.md)

- [编写 AVStream 微型驱动程序](writing-an-avstream-minidriver.md)

## <a name="see-also"></a>另请参阅

[流媒体设备驱动程序参考](/windows-hardware/drivers/ddi/_stream/index)
