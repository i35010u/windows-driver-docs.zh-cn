---
title: 为 Windows 8.1 编写位置传感器驱动程序
description: 为 Windows 8.1 编写位置传感器驱动程序
ms.assetid: 18852282-6529-4934-a448-b699e01987de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7642faf1d1a633ce3c2052c486925cb0fe4d4f08
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363633"
---
# <a name="writing-a-location-sensor-driver-for-windows-81"></a>为 Windows 8.1 编写位置传感器驱动程序

本部分提供了用于编写提供位置数据的设备的驱动程序的具体指南。 除了在本部分中包含的信息，位置驱动程序作者必须还了解和应用中提供的信息[编写传感器设备驱动程序](https://docs.microsoft.com/windows-hardware/drivers/sensors/writing-a-sensor-device-driver)。

传感器和位置平台提供了 Windows 位置 API，使软件开发人员能够轻松地将位置功能添加到他们的程序。 如果你正在编写位置传感器的驱动程序，必须了解如何使驱动程序与位置 API 兼容，并遵循中的准则[能力和性能的位置驱动程序指南](location-driver-guidelines-for-power-and-performance.md)。

## <a name="windows-hardware-certification-program-requirements"></a>Windows 硬件认证计划要求

Windows 硬件认证计划使硬件制造商以接收其设备满足所需的标准 Windows 所使用的证书。 认证计划描述为位置传感器的要求和其他类型的传感器。 应使您符合所有认证计划要求的位置传感器驱动程序。 这些要求包括：

-   位置传感器必须支持所需的数据和传感器属性集。

-   对于至少一个内置数据报表类型的位置传感器必须支持所需的数据字段。

通常情况下，此 WDK 文档中的建议与匹配的认证计划要求。 但是，你必须创建想要提交以供审批的传感器驱动程序时查看官方认证计划文档。 有关 Windows 硬件认证计划的详细信息，请参阅[Windows 硬件开发人员中心](https://developer.microsoft.com/en-us/windows/hardware)网站。

## <a name="location-api-requirements"></a>位置 API 要求

使用与任何其他类别的传感器的相同驱动程序模型和类扩展创建为位置传感器驱动程序。 最小值，以便为位置传感器，驱动程序必须：

-   标识为属于位置类别位置传感器。

-   传感器类型设置为位置传感器类型之一。

-   确定传感器提供的位置报告数据字段。

-   支持所需的属性。

-   为在请求时提供数据。

-   管理状态转换。

-   引发数据更新和状态更改事件。

本部分的其余部分将介绍这些最低要求

## <a name="identifying-the-category"></a>标识类别

当通过调用[ **ISensorDriver::OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)，将**WPD\_功能\_对象\_类别**属性值设置为**传感器\_类别\_位置**。 下面的代码示例演示如何将此常量的指针通过设置[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)名为 pValues。

```cpp
hr = pValues->SetGuidValue(WPD_FUNCTIONAL_OBJECT_CATEGORY, SENSOR_CATEGORY_LOCATION);
```

## <a name="setting-the-location-sensor-type"></a>设置位置传感器类型

当通过调用[ **ISensorDriver::OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)，将**传感器\_属性\_类型**到正确的属性值值。 下面的代码示例演示如何使用设置的传感器类型**传感器\_类型\_位置\_GPS**常量的指针通过[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)名为 pValues。

```cpp
hr = pValues->SetGuidValue(SENSOR_PROPERTY_TYPE, SENSOR_TYPE_LOCATION_GPS);
```

## <a name="identifying-the-supported-data-fields"></a>确定支持的数据字段

位置 API 定义了两种类型的位置报告。 这些是组织位置的数据的对象。 经纬度报表包含纬度、 经度和海拔高度数据字段，以及数据字段包含错误的范围信息。 市政地址报告包含街道地址的数据字段，例如城市和邮政编码。 位置驱动程序必须至少一个两个数据报告类型支持所需的数据字段。

若要支持经纬度报表，以下数据字段是必需的：

-   传感器\_数据\_类型\_纬度\_度
-   传感器\_数据\_类型\_经度\_度
-   SENSOR\_DATA\_TYPE\_ERROR\_RADIUS\_METERS

若要支持市政地址报表，至少一个以下数据字段是必需的：

-   传感器\_数据\_类型\_国家/地区\_区域

(若要查看完整的平台定义的位置数据字段集，请参阅[**传感器\_类别\_位置**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-category-loc)中[Windows 传感器引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)部分。)

当通过调用[ **ISensorDriver::OnGetSupportedDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupporteddatafields)，将添加到受支持的数据字段属性键常数[IPortableDeviceKeyCollection](https://go.microsoft.com/fwlink/p/?linkid=131484)通过返回的*ppSupportedDataFields*参数。 下面的代码示例演示如何邮政编码数据字段添加到[IPortableDeviceKeyCollection](https://go.microsoft.com/fwlink/p/?linkid=131484)通过一个名为 pKeyCollection 变量。

```cpp
pKeyCollection->Add(SENSOR_DATA_TYPE_POSTALCODE);
```

## <a name="support-the-required-properties"></a>支持所需的属性

其他传感器驱动程序，如位置驱动程序提供有关传感器本身通过一组属性的信息。 Windows 硬件认证计划指定的最小的所需的位置传感器必须支持的属性集。 有关传感器属性、 它们的含义和哪些属性所需的传感器驱动程序的详细信息，请参阅[**传感器属性**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-properties)。 以下列表包含所需的属性：

-   WPD\_功能\_对象\_类别

-   传感器\_属性\_类型

-   传感器\_属性\_状态

-   传感器\_属性\_的永久\_UNIQUE\_ID

-   传感器\_属性\_制造商

-   传感器\_属性\_模型

-   传感器\_属性\_串行\_数

-   传感器\_属性\_友好\_名称

-   传感器\_属性\_MIN\_报表\_间隔

-   传感器\_属性\_当前\_报表\_间隔

-   传感器\_属性\_位置\_所需\_准确性

## <a name="providing-data"></a>提供数据

位置驱动程序通过相同的机制与其他传感器驱动程序提供数据。 传感器类扩展，即调用通过驱动程序[ **ISensorDriver::OnGetDataFields** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetdatafields)和驱动程序返回的值通过*ppDataValues*参数。

以下要求适用于从位置传感器提供数据：

-   提供这两个数据同步请求通过和通过[引发事件](https://docs.microsoft.com/windows-hardware/drivers/sensors/raising-events)。

-   保持最新的数据报表的副本。 如果在请求时，新的数据不可用，则返回缓存的报表。 不会更新的时间戳。

-   未提供值的传感器\_数据\_类型\_纬度\_度和传感器\_数据\_类型\_经度\_度超出范围实际的纬度和经度的范围。

-   不报告值的传感器\_数据\_类型\_错误\_RADIUS\_是零个或更少的指标。

-   将值设置为传感器\_数据\_类型\_国家/地区\_区域保存到有效的 ISO 3166 1-alpha-2 国家/地区代码。

-   如果您的驱动程序支持纬度/经度和市政地址报表，这些报表中的位置数据应对应于同一物理位置。

下表描述了[传感器数据字段](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-categories--types--and-data-fields)，对应于位置 API 数据报表的字段。 当某一位置提供数据的报表时，请使用这些数据字段常量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>传感器常量</th>
<th>位置 API 方法和属性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_ADDRESS1</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157816" data-raw-source="[ICivicAddressReport::GetAddressLine1](https://go.microsoft.com/fwlink/p/?linkid=157816)">ICivicAddressReport::GetAddressLine1</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157817" data-raw-source="[LocationDisp.DispCivicAddressReport.AddressLine1](https://go.microsoft.com/fwlink/p/?linkid=157817)">LocationDisp.DispCivicAddressReport.AddressLine1</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_ADDRESS2</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157818" data-raw-source="[ICivicAddressReport::GetAddressLine2](https://go.microsoft.com/fwlink/p/?linkid=157818)">ICivicAddressReport::GetAddressLine2</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157820" data-raw-source="[LocationDisp.DispCivicAddressReport.AddressLine2](https://go.microsoft.com/fwlink/p/?linkid=157820)">LocationDisp.DispCivicAddressReport.AddressLine2</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157823" data-raw-source="[ILatLongReport::GetAltitudeError](https://go.microsoft.com/fwlink/p/?linkid=157823)">ILatLongReport::GetAltitudeError</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157824" data-raw-source="[LocationDisp.DispLatLongReport.AltitudeError](https://go.microsoft.com/fwlink/p/?linkid=157824)">LocationDisp.DispLatLongReport.AltitudeError</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157825" data-raw-source="[ILatLongReport::GetAltitude](https://go.microsoft.com/fwlink/p/?linkid=157825)">ILatLongReport::GetAltitude</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157827" data-raw-source="[LocationDisp.DispLatLongReport.Altitude](https://go.microsoft.com/fwlink/p/?linkid=157827)">LocationDisp.DispLatLongReport.Altitude</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_CITY</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157828" data-raw-source="[ICivicAddressReport::GetCity](https://go.microsoft.com/fwlink/p/?linkid=157828)">ICivicAddressReport::GetCity</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157830" data-raw-source="[LocationDisp.DispCivicAddressReport.City](https://go.microsoft.com/fwlink/p/?linkid=157830)">LocationDisp.DispCivicAddressReport.City</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.CivicAddress#Windows_Devices_Geolocation_CivicAddress_City" data-raw-source="[Windows.Devices. Geolocation.CivicAddress](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.CivicAddress#Windows_Devices_Geolocation_CivicAddress_City)">Windows.Devices。Geolocation.CivicAddress</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_COUNTRY_REGION</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157831" data-raw-source="[ICivicAddressReport::GetCountryRegion](https://go.microsoft.com/fwlink/p/?linkid=157831)">ICivicAddressReport::GetCountryRegion</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157832" data-raw-source="[LocationDisp.DispCivicAddressReport.CountryRegion](https://go.microsoft.com/fwlink/p/?linkid=157832)">LocationDisp.DispCivicAddressReport.CountryRegion</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_ERROR_RADIUS_METERS</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157834" data-raw-source="[ILatLongReport::GetErrorRadius](https://go.microsoft.com/fwlink/p/?linkid=157834)">ILatLongReport::GetErrorRadius</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157835" data-raw-source="[LocationDisp.DispLatLongReport.ErrorRadius](https://go.microsoft.com/fwlink/p/?linkid=157835)">LocationDisp.DispLatLongReport.ErrorRadius</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_LATITUDE_DEGREES</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157836" data-raw-source="[ILatLongReport::GetLatitude](https://go.microsoft.com/fwlink/p/?linkid=157836)">ILatLongReport::GetLatitude</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157839" data-raw-source="[LocationDisp.DispLatLongReport.Latitude](https://go.microsoft.com/fwlink/p/?linkid=157839)">LocationDisp.DispLatLongReport.Latitude</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_LONGITUDE_DEGREES</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157840" data-raw-source="[ILatLongReport::GetLongitude](https://go.microsoft.com/fwlink/p/?linkid=157840)">ILatLongReport::GetLongitude</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157841" data-raw-source="[LocationDisp.DispLatLongReport.Longitude](https://go.microsoft.com/fwlink/p/?linkid=157841)">LocationDisp.DispLatLongReport.Longitude</a></p></td>
</tr>
<tr class="even">
<td><p><strong>SENSOR_DATA_TYPE_POSTALCODE</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157842" data-raw-source="[ICivicAddressReport::GetPostalCode](https://go.microsoft.com/fwlink/p/?linkid=157842)">ICivicAddressReport::GetPostalCode</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157844" data-raw-source="[LocationDisp.DispCivicAddressReport.PostalCode](https://go.microsoft.com/fwlink/p/?linkid=157844)">LocationDisp.DispCivicAddressReport.PostalCode</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SENSOR_DATA_TYPE_STATE_PROVINCE</strong></p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157846" data-raw-source="[ICivicAddressReport::GetStateProvince](https://go.microsoft.com/fwlink/p/?linkid=157846)">ICivicAddressReport::GetStateProvince</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=157847" data-raw-source="[LocationDisp.DispCivicAddressReport.StateProvince](https://go.microsoft.com/fwlink/p/?linkid=157847)">LocationDisp.DispCivicAddressReport.StateProvince</a></p></td>
</tr>
</tbody>
</table>

## <a name="managing-state-transitions"></a>管理状态转换

在任何时候，传感器驱动程序可以在多个状态之一。 通过定义传感器状态[ **SensorState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)枚举。 若要正确使用位置 API，位置传感器必须遵循这些规则用于处理状态转换。

-   始终启动在传感器\_状态\_初始化状态，但不是会引发在启动时的状态更改事件。

-   该驱动程序应转换从传感器\_状态\_初始化到传感器\_状态\_已准备就绪数据是否可用。
-   该驱动程序应转换回传感器\_状态\_初始化时，驱动程序不具有到报表的当前数据。 该驱动程序应确定当发生此转换。 如果你丢失了信号，但仍有办法来提供有效的数据，会保留在传感器\_状态\_就绪状态。
-   始终引发事件的正确顺序。 首先，确定数据已可用。 然后，引发状态更改事件。 最后，会引发数据更新事件。

-   始终引发状态更改事件驱动程序的状态更改时。

-   位置 API 不使用处于以下状态的传感器数据：传感器\_状态\_否\_数据、 传感器\_状态\_不\_可用、 传感器\_状态\_错误。

下表所述位置传感器驱动程序的各种传感器状态...

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>含义</th>
<th>位置 API 状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SENSOR_STATE_READY</p></td>
<td><p>传感器驱动程序可以提供具有完整且准确的数据的新位置报告。</p>
<p>例如，Wi-fi 或移动运营商提供连接和工作或 GPS 传感器已修复。</p>
<p>已使用来自三边转换传感器数据来确定位置的 GPS 驱动程序具有此状态。</p></td>
<td><p>REPORT_RUNNING</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_STATE_INITIALIZING</p></td>
<td><p>传感器驱动程序尝试获取修补程序。 传感器驱动程序应将此状态转换到 SENSOR_STATE_READY 后处于锁定状态修补程序和跟踪。</p>
<p>例如，Wi-fi 提供程序正在寻找的 Internet 连接、 移动运营商提供寻找无线电收发器，或 GPS 传感器获得的修补程序。</p>
<p>在尝试重新获取修补程序时，GPS 传感器应重新进入此状态。</p></td>
<td><p>REPORT_INITIALIZING</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_STATE_NO_DATA</p></td>
<td><p>位置提供程序可用，但不能提供位置数据。</p>
<p>例如，Wi-fi 提供程序有权访问 Internet，但数据库没有任何位置数据。</p></td>
<td><p>REPORT_ERROR</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_STATE_NOT_AVAILABLE</p></td>
<td><p>位置提供程序用于获取数据的功能被禁用。</p>
<p>如果电话功能已关闭，GPS 传感器可能会处于此状态。</p></td>
<td><p>REPORT_ERROR</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_STATE_ERROR</p></td>
<td><p>传感器遇到重大错误。 传感器可以恢复处于此状态，但不是知道恢复时间范围。</p></td>
<td><p>REPORT_ERROR</p></td>
</tr>
</tbody>
</table>

 

下图显示了状态转换中的位置传感器可能会发生。![状态转换](images/gps-state-transitions.png)

## <a name="raising-data-updated-and-state-changed-events"></a>引发数据更新和状态更改事件

位置 API，需要位置传感器，例如 GPS 传感器，若要引发事件提供数据和状态更改信息。 有关提升传感器事件的详细信息，请参阅[有关传感器驱动程序事件](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-driver-events)。

时引发这些事件，位置驱动程序必须遵循下列规则：

-   通过调用传感器类扩展引发状态更改事件[ **ISensorClassExtension::PostStateChange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)方法。 不要调用[**得到**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)以引发状态更改事件。

-   通过调用引发数据更新事件[**得到**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)。
-   仅当数据为最新且精确，则引发数据更新事件。

-   不会引发数据更新事件两次。 这意味着，不应使用缓存的数据引发数据更新事件。 可以为数据提供对同步请求响应中的缓存的数据。

-   发送事件的纬度/经度报表时，始终包含所有所需的数据字段。

-   始终引发数据更新事件，当传感器准确性发生更改时。

-   传感器报告的有效值\_数据\_类型\_错误\_RADIUS\_之前引发事件和更改值的传感器的计量\_属性\_到传感器状态\_状态\_准备就绪。

-   不提供不完整的数据的报表。

-   您可能没有所需的数据字段，例如 GPS 传感器时丢失其修补程序的当前数据。 在这种情况下，仍可能要提供有关更新到扩展的数据字段，如传感器的通知\_数据\_类型\_NMEA\_句子。 若要提供此类通知，必须使用自定义事件类型，并引发仅自定义事件之前所需的数据字段的数据变得可用。 有关如何定义自定义类型的信息，请参阅[定义的自定义值的常量](https://docs.microsoft.com/windows-hardware/drivers/sensors/defining-custom-values-for-constants)。

## <a name="related-topics"></a>相关主题

[能力和性能的位置驱动程序指南](location-driver-guidelines-for-power-and-performance.md)  
