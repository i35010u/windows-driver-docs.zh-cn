---
title: 活动检测传感器数据字段
description: 本主题提供有关特定于活动检测传感器的数据字段的信息。
ms.assetid: D123C082-9E20-44C2-A9F2-DAC0E09F61B7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0359486281af6b79d9f16975241f4c20ac1d6f15
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824282"
---
# <a name="activity-detection-sensor-data-fields"></a>活动检测传感器数据字段


本主题提供有关特定于活动检测传感器的数据字段的信息。

下表显示了数据字段。 有关 "**类型**" 列中显示的数据类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|在任务栏的搜索框中键入|必需/可选|描述|
| --- | --- | --- | --- |
|PKEY_SensorData_CurrentActivityState|VT_UI4|必需|当前活动状态的指示，表示为[<strong>ACTIVITY_STATE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)类型的值。|
|PKEY_SensorData_CurrentActivityStateConfidence_Percentage|VT_UI2|必需|指示当前活动状态的传感器的置信度级别。|
|PKEY_SensorData_SubscribedActivityStates|VT_UI4|必需|指示订阅的活动状态，表示为[<strong>ACTIVITY_STATE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)类型的值。|
|PKEY_SensorData_ActivityStream|VT_BOOL|必需|如果活动流可用，则设置为 TRUE 的布尔值。|
|PKEY_SensorData_ConfidenceThreshold_Percentage|VT_UI2|必需|传感器置信度的阈值。|
 

## <a name="related-topics"></a>相关主题


[**活动\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)

[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






