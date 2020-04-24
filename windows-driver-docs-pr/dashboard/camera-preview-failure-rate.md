---
title: 相机预览失败次数百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为相机设备无法使用预览功能的实例所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 32e6692b5b895ecb11224d62561e306a083d37a7
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "71017076"
---
# <a name="percent-of-camera-preview-failures"></a>相机预览失败次数百分比

## <a name="description"></a>说明

尝试捕获图像时，设备可预览即将捕获的图像。 如果预览功能失败，用户将看不到相机的透视图，并可能无法拍照以将图像作为照片保存。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小总体数量 |10 个实例|
|通过标准 |<= 8% 的预览实例导致故障|
|度量 ID |16998893|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为相机设备无法使用预览功能的实例所占的百分比  。

   a. 单个设备中可以有多种通过度量进行计数的预览实例。

2. 实例类型：

   a. 成功的预览事件 = 0% 失败 

       MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PREVIEW_STARTED) HRESULT == 0
       MFCaptureEnginePreviewSinkFirstFrame (MF_CAPTURE_ENGINE_PREVIEW_STARTED)

   b. 失败的预览事件 = 100% 失败 

       MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PREVIEW_STARTED) HRESULT != 0
      或者成功地预览事件后跟  ：

       MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_ERROR)
       MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PREVIEW_STOPPED) > 1000ms
       MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_PREVIEW_STARTED) HRESULT != 0

### <a name="final-calculation"></a>最终计算

相机预览失败率 = 平均值（所有实例） 