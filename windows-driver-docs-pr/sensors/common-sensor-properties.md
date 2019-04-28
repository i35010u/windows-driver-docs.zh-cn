---
title: 通用传感器属性
description: 本主题介绍常见的所有传感器的传感器属性。
ms.assetid: 3E4DD221-BA8E-446E-BA7A-EF84DFED332F
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7aa167e2b04935467d8638ea909372dc4847624a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330104"
---
# <a name="common-sensor-properties"></a>通用传感器属性


本主题介绍常见的所有传感器的传感器属性。

下表显示通用属性。 有关类型列中显示的类型的详细信息，请参阅[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>属性键</th>
<th>在任务栏的搜索框中键入</th>
<th>访问 （R/O，R/W）</th>
<th>必需/可选</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_Sensor_Type</p></td>
<td><p>VT_CLSID</p></td>
<td><p>R/O</p></td>
<td><p>必需</p></td>
<td><p>传感器的类型。 GUID 将包括与 Windows 传感器 (例如，SENSOR_TYPE_ACCELEROMETER_3D) 相同的格式。 有关传感器类型的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/dn946707" data-raw-source="[Sensor type GUIDs](https://msdn.microsoft.com/library/windows/hardware/dn946707)">传感器类型 Guid</a>。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_Sensor_State</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必需</p></td>
<td><p>传感器的状态。 有关传感器状态的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/dn946703" data-raw-source="[&lt;strong&gt;SENSOR_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn946703)"> <strong>SENSOR_STATE</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_MinimumDataInterval_Ms</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必需</p></td>
<td><p>传感器数据生成报告的硬件支持的最小时间间隔 （以毫秒为单位）。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_Sensor_MaximumDataFieldSize_Bytes</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必需</p></td>
<td><p>ReadFile 调用中返回的最大大小。 ReadFile 调用允许本机 API 来分配缓冲区来存放数据的任何字段。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_Power_Milliwatts</p></td>
<td><p>VT_R4</p></td>
<td><p>R/O</p></td>
<td><p>可选</p></td>
<td><p>表示单位为毫瓦传感器的强大功能。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorHistory_MaxSize_Bytes</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>可选</p>
<p>但需要，如果传感器支持历史记录。</p></td>
<td><p>传感器历史记录数据，以字节为单位的最大大小。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorHistory_Interval_Ms</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>可选</p>
<p>但需要，如果传感器支持历史记录。</p></td>
<td><p>传感器历史记录采样间隔，以毫秒为单位。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorHistory_MaximumRecordSize_Bytes</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>可选</p>
<p>但需要，如果传感器支持历史记录。</p></td>
<td><p>以字节为单位表示的最大记录大小。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_FifoReservedSize_Samples</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>可选</p>
<p>但需要，如果传感器支持批处理。</p></td>
<td><p>为批处理此传感器前先出 (FIFO) 缓冲区中保留的事件数。 这可以保证最低数目的事件。 如果此值为零，则不能保证传感器将执行批处理。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_Sensor_FifoMaxSize_Samples</p></td>
<td><p>VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>可选</p>
<p>但需要，如果传感器支持批处理。</p></td>
<td><p>最大可能 FIFO 中成批处理的事件数。 如果此值为零，则不支持批处理传感器。 自可由多个传感器共享先进先出的批处理的事件的实际数目可能比此数值较小。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_Sensor_WakeCapable</p></td>
<td><p>VT_BOOL</p></td>
<td><p>R/O</p></td>
<td><p>可选</p>
<p>但需要，如果传感器支持批处理。</p></td>
<td><p>指示是否支持唤醒的传感器。</p>
<p>当传感器支持传感器批处理时，这应设置为 VARIANT_TRUE，这是如果先进先出已满时，传感器可以唤醒应用程序处理器。 并且，当传感器无法唤醒应用程序处理器，应为 VARIANT_FALSE，设置此值。 在这种情况下，此属性的状态将指示从连接待机状态唤醒的传感器的能力。</p>
<p>如果从 SX 唤醒传感器支持唤醒从 SX 系统，此属性应设置为 VARIANT_TRUE，如果它不支持，则此属性应设置为 VARIANT_FALSE。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idnotespanspan-idnotespanspan-idnotespannote"></a><span id="Note"></span><span id="note"></span><span id="NOTE"></span>请注意


支持批处理的数据的传感器驱动程序必须报告以下常见传感器属性：

-   PKEY\_Sensor\_FifoReservedSize\_Samples

-   PKEY\_Sensor\_FifoMaxSize\_Samples

-   PKEY\_Sensor\_WakeCapable

从 Windows 10，版本 1511，开始支持现已可供实现数据批处理使用的 HID 传感器类驱动程序。 有关此信息，请参阅[传感器批处理控件](sensor-batching-for-power-saving-.md)。

请参阅[EvtSensorSetBatchLatency](https://msdn.microsoft.com/library/windows/hardware/mt219125)有关回调函数的信息与数据批处理。

使用传感器的附加功能来唤醒的 CPU 和操作系统从 SX 状态，主键\_传感器\_WakeCapable 还用作枚举属性，可从要找出传感器是否的即插即用驱动程序存储区查询能够从 SX 系统除了唤醒从连接待机系统唤醒。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


当客户端驱动程序报告了以下属性时，必须使用客户端驱动程序**CollectionsListGetMarshalledSizeWithoutSerialization**而不是**CollectionsListGetMarshalledSize**:

-   PKEY\_SensorHistory\_MaxSize\_Bytes

-   PKEY\_SensorHistory\_MaximumRecordSize\_Bytes

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[EvtSensorSetBatchLatency](https://msdn.microsoft.com/library/windows/hardware/mt219125)

[PROPVARIANT 结构](https://go.microsoft.com/fwlink/p/?linkid=313395)

[传感器属性](sensor-properties2.md)

[**SENSOR\_STATE**](https://msdn.microsoft.com/library/windows/hardware/dn946703)

[Guid 的传感器类型](https://msdn.microsoft.com/library/windows/hardware/dn946707)

 

 






