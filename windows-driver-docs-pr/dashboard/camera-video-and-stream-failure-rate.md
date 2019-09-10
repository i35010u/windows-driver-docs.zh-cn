---
title: 相机视频和流故障次数百分比
description: 该度量将来自 7 天滑动窗口的遥测数据聚合为相机设备无法使用视频和流式处理功能的实例所占的百分比
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 996ab915b7ea098622275f1762dfaf353b14d945
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70224029"
---
# <a name="percent-of-camera-video-and-stream-failures"></a>相机视频和流故障次数百分比

## <a name="description"></a>描述

若要捕获相机的视频流，计算机必须将计算机透视图连续存储到视频文件中。 如果视频和流式处理功能发生故障，用户将无法捕获相机的透视图，可能会丢失尚未保存的视频。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众 |Standard|
|时间段 |7 天滑动窗口|
|度量标准 |实例的聚合|
|最小总体数量 |10 个实例|
|通过标准 |<= 10% 的视频和流式处理实例导致故障|
|度量 ID |16999057|

## <a name="calculation"></a>计算

1. 该度量将来自 7 天滑动窗口的遥测数据聚合为相机设备无法使用视频和流式处理功能的实例所占的百分比  。

   a. 单个设备中可以有多种通过度量进行计数的视频和流式处理实例。

2. 实例类型：

   a. 成功的视频和流式处理事件 = 0% 故障   

       i. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_RECORD_STARTED)

   b. 失败的视频和流式处理事件 = 100% 故障 

         i. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_ERROR)
        ii. MFCaptureEngineOnEvent (MF_CAPTURE_ENGINE_RECORD_STOPPED)
       iii. MFCaptureEngineSessionStop
        iv. OnEvent_RecordStop_Failure
         v. Timed Out

### <a name="final-calculation"></a>最终计算

相机视频和流式处理故障率 = 平均值（所有实例） 