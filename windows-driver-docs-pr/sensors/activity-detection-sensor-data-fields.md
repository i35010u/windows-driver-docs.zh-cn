---
title: 活动检测传感器数据字段
description: 本主题提供有关特定于活动检测传感器的数据字段的信息。
ms.assetid: D123C082-9E20-44C2-A9F2-DAC0E09F61B7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: dd92a77500b7e36f7c9068a5b2e73e1c8fa972fd
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009877"
---
# <a name="activity-detection-sensor-data-fields"></a>活动检测传感器数据字段


本主题提供有关特定于活动检测传感器的数据字段的信息。

下表显示了数据字段。 有关 " **类型** " 列中显示的数据类型的详细信息，请参阅 [PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

|属性键|类型|必需/可选|说明|
| --- | --- | --- | --- |
|PKEY_SensorData_CurrentActivityState|VT_UI4|必需|当前活动状态的指示，表示为类型 [<strong>ACTIVITY_STATE</strong>](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)的值。|
|PKEY_SensorData_CurrentActivityStateConfidence_Percentage|VT_UI2|必需|指示当前活动状态的传感器的置信度级别。|
|PKEY_SensorData_SubscribedActivityStates|VT_UI4|必需|指示已订阅活动状态，表示为类型 [<strong>ACTIVITY_STATE</strong>](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)的值。|
|PKEY_SensorData_ActivityStream|VT_BOOL|必需|如果活动流可用，则设置为 TRUE 的布尔值。|
|PKEY_SensorData_ConfidenceThreshold_Percentage|VT_UI2|必需|传感器置信度的阈值。|
 

## <a name="related-topics"></a>相关主题


[**活动 \_ 状态**](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)

[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

