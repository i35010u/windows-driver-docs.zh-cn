---
title: 枚举属性
description: 本主题介绍中即插即用驱动程序存储区提供了静态传感器属性。
ms.assetid: E4663410-375F-48B9-A9E4-6E608FA8D2FF
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5bcd0470d4ae7a3498b5bdfe00df7034b810564e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386186"
---
# <a name="enumeration-properties"></a>枚举属性


本主题介绍中即插即用驱动程序存储区提供了静态传感器属性。

下表显示了静态传感器属性。 类扩展 (CX) 将写入每个传感器的这些属性时[SensorsCxSensorCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensorcreate)调用。 客户端应用程序可以使用这些属性来搜索 Windows 设备上的传感器。

有关详细信息中所示的数据类型**类型**列中，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性键</th>
<th>在任务栏的搜索框中键入</th>
<th>必需/可选</th>
<th><strong>说明</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Type</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必需</p></td>
<td><p>标识类型的传感器的 GUID。 有关传感器类型的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants" data-raw-source="[Sensor type GUIDs](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)">传感器类型 Guid</a>。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_Category</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必需</p></td>
<td><p>传感器类别中。 这是为了向后兼容性与桌面 v1 堆栈，其中它是一项要求。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_ConnectionType</p></td>
<td><p>VT_UI4</p></td>
<td><p>可选</p>
<p>所需的环境光线传感器和加速感应器</p></td>
<td><p>传感器连接类型。 传感器连接类型可以是集成、 附加或外部。</p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002" data-raw-source="[&lt;strong&gt;SensorConnectionType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002)"> <strong>SensorConnectionType</strong> </a>枚举。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_IsPrimary</p></td>
<td><p>VT_BOOL</p></td>
<td><p>可选</p></td>
<td><p>指示这是主要的传感器。 这具有默认值为 false，如果未设置。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Name</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>所需的自定义传感器。</p></td>
<td><p>传感器的名称。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_Manufacturer</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>必需</p></td>
<td><p>传感器制造商。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Model</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>必需</p></td>
<td><p>传感器模型。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_PersistentUniqueId</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必需</p></td>
<td><p>标识传感器的 GUID。 此值必须是唯一的设备上的同一模型的每个传感器。 此要求适用于这两个内部和外部连接的传感器。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_VendorDefinedSubType</p></td>
<td><p>VT_CLSID</p></td>
<td><p>所需的自定义传感器。</p></td>
<td><p>标识已由供应商定义的传感器类别子类型的 GUID。</p>
<p>对于非自定义传感器，这不是必需。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_SensorData_LightLevel_AutoBrightnessPreferred</p></td>
<td><p>VT_BOOL</p></td>
<td><p>可选</p></td>
<td><p>光线传感器是自动亮度的首选。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_SensorData_LightLevel_ColorCapable</p></td>
<td><p>VT_BOOL</p></td>
<td><p>可选。 如果支持色度和浅温度，必需。</p></td>
<td><p>光线传感器支持浅色温度和/或色度 x / y。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

[**SensorConnectionType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002)

[SensorsCxSensorCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensorcreate)

[传感器属性](sensor-properties2.md)

[Guid 的传感器类型](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)

 

 






