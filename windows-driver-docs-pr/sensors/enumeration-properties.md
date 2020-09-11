---
title: 枚举属性
description: 本主题介绍 PnP 驱动程序存储区中可用的静态传感器属性。
ms.assetid: E4663410-375F-48B9-A9E4-6E608FA8D2FF
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: b521c9db71ac27d1f4e7aa2e9d16aacbf1d50db2
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010281"
---
# <a name="enumeration-properties"></a>枚举属性


本主题介绍 PnP 驱动程序存储区中可用的静态传感器属性。

下表显示了静态传感器属性。 调用 [SensorsCxSensorCreate](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensorcreate) 时，) 扩展 (CX 为每个传感器写入这些属性。 客户端应用程序可以使用这些属性在 Windows 设备上搜索传感器。

有关 " **类型** " 列中显示的数据类型的详细信息，请参阅 [PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

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
<th>类型</th>
<th>必需/可选</th>
<th><strong>描述</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Type</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必需</p></td>
<td><p>标识传感器类型的 GUID。 有关传感器类型的详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants" data-raw-source="[Sensor type GUIDs](./about-sensor-constants.md)">传感器类型 guid</a>。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_Category</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必需</p></td>
<td><p>传感器类别。 这是为了在需要时与桌面 v1 堆栈向后兼容。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_ConnectionType</p></td>
<td><p>VT_UI4</p></td>
<td><p>可选</p>
<p>对于环境光线传感器和加速感应器是必需的</p></td>
<td><p>Senor 连接类型。 传感器连接类型可集成、附加或外部。</p>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002" data-raw-source="[&lt;strong&gt;SensorConnectionType&lt;/strong&gt;](/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002)"><strong>SensorConnectionType</strong></a> 枚举。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_IsPrimary</p></td>
<td><p>VT_BOOL</p></td>
<td><p>可选</p></td>
<td><p>指示这是主传感器。 如果未设置，则此值的默认值为 false。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Name</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>对于自定义传感器是必需的。</p></td>
<td><p>传感器的名称。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_Manufacturer</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>必需</p></td>
<td><p>传感器的制造商。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_Model</p></td>
<td><p>VT_LPWSTR</p></td>
<td><p>必需</p></td>
<td><p>传感器的模型。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_Sensor_PersistentUniqueId</p></td>
<td><p>VT_CLSID</p></td>
<td><p>必需</p></td>
<td><p>标识传感器的 GUID。 对于设备上相同型号的每个传感器，此值必须是唯一的。 此要求适用于内部和外部连接的传感器。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_Sensor_VendorDefinedSubType</p></td>
<td><p>VT_CLSID</p></td>
<td><p>对于自定义传感器是必需的。</p></td>
<td><p>标识供应商定义的传感器类别子类型的 GUID。</p>
<p>对于非自定义传感器，这不是必需的。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_SensorData_LightLevel_AutoBrightnessPreferred</p></td>
<td><p>VT_BOOL</p></td>
<td><p>可选</p></td>
<td><p>光源传感器是自动亮度的首选。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_SensorData_LightLevel_ColorCapable</p></td>
<td><p>VT_BOOL</p></td>
<td><p>可选。 如果支持 chromaticity 和轻型温度，则是必需的。</p></td>
<td><p>光源传感器支持轻型温度和/或 chromaticity x/y。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

[**SensorConnectionType**](/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0002)

[SensorsCxSensorCreate](/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensorcreate)

[传感器属性](sensor-properties2.md)

[传感器类型 Guid](./about-sensor-constants.md)

 

