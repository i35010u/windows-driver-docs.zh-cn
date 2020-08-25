---
title: 为 Windows 8.1 编写位置传感器驱动程序
description: 为 Windows 8.1 编写位置传感器驱动程序
ms.assetid: 18852282-6529-4934-a448-b699e01987de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a7aceacedfe2b8a01a9e825dd6abc8fb0aaf9a2
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850275"
---
# <a name="writing-a-location-sensor-driver-for-windows-81"></a>为 Windows 8.1 编写位置传感器驱动程序

传感器和位置平台提供 Windows 定位 API，使软件开发人员能够轻松地将位置功能添加到其程序中。 如果要为位置传感器编写驱动程序，则必须了解如何使驱动程序与位置 API 兼容，并遵循 [位置驱动程序指南中有关电源和性能](location-driver-guidelines-for-power-and-performance.md)的指导原则。

## <a name="windows-hardware-certification-program-requirements"></a>Windows 硬件认证计划要求

Windows 硬件认证计划允许硬件制造商接收其设备符合使用 Windows 所需标准的认证。 认证计划描述位置传感器和其他类型传感器的要求。 你应使你的位置传感器驱动程序符合所有认证计划要求。 这些要求包括：

- 位置传感器必须支持所需的数据和传感器属性集。

- 位置传感器必须支持至少一个内置数据报表类型所需的数据字段。

通常，此 WDK 文档中的建议与认证计划要求相匹配。 但是，在创建要提交以供审批的传感器驱动程序时，必须查看官方认证计划文档。 有关 Windows 硬件认证计划的详细信息，请参阅 [Windows 硬件开发人员中心](https://developer.microsoft.com/windows/hardware) 网站。

## <a name="location-api-requirements"></a>位置 API 要求

使用与任何其他类别的传感器相同的驱动程序模型和类扩展，为位置传感器创建驱动程序。 驱动程序必须至少执行以下操作：

- 将位置传感器标识为属于 "位置" 类别。

- 将传感器类型设置为位置传感器类型之一。

- 标识传感器提供的位置报表数据字段。

- 支持必需的属性。

- 在请求数据时提供数据。

- 管理状态转换。

- 引发数据更新和状态更改事件。

本部分的其余部分介绍了这些最低要求

## <a name="identifying-the-category"></a>标识类别

通过 [**ISensorDriver：： OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)调用此方法时，请将 **WPD \_ 功能 \_ 对象 \_ 类别** 属性值设置为 **传感器 \_ 类别 \_ 位置**。 下面的代码示例演示如何将此常量设置为指向名为 pValues 的 [IPortableDeviceValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues) 的指针。

```cpp
hr = pValues->SetGuidValue(WPD_FUNCTIONAL_OBJECT_CATEGORY, SENSOR_CATEGORY_LOCATION);
```

## <a name="setting-the-location-sensor-type"></a>设置位置传感器类型

通过 [**ISensorDriver：： OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)调用它时，请将 " **传感器 \_ 属性 \_ 类型** " 属性值设置为正确的值。 下面的代码示例演示如何使用 **传感器 \_ 类型 \_ 位置 \_ GPS** 常量通过指向名为 pValues 的 [IPortableDeviceValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues) 的指针来设置传感器类型。

```cpp
hr = pValues->SetGuidValue(SENSOR_PROPERTY_TYPE, SENSOR_TYPE_LOCATION_GPS);
```

## <a name="identifying-the-supported-data-fields"></a>标识支持的数据字段

Location API 定义两种类型的位置报告。 这些是组织位置数据的对象。 经纬度报表包含纬度、经度和海拔数据字段，以及包含错误范围信息的数据字段。 市政地址报表包含街道地址数据字段，如城市和邮政编码。 您的位置驱动程序必须支持这两种数据报表类型中的至少一种所需的数据字段。

若要支持经纬度报表，需要以下数据字段：

- 传感器 \_ 数据 \_ 类型 \_ 纬度 \_ 度

- 传感器 \_ 数据 \_ 类型 \_ 经度 \_ 度数

- 传感器 \_ 数据 \_ 类型 \_ 错误 \_ RADIUS \_ 计量

若要支持市政地址报表，至少需要以下数据字段之一：

- 传感器 \_ 数据 \_ 类型 \_ 国家/ \_ 地区

若要查看完整的平台定义位置数据字段集，请参阅[Windows 传感器参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)部分中的[**传感器 \_ 类别 \_ 位置**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-category-loc)。

通过[**ISensorDriver：： OnGetSupportedDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupporteddatafields)调用它们时，将支持的数据字段属性键常量添加到通过*ppSupportedDataFields*参数返回的[IPortableDeviceKeyCollection](https://docs.microsoft.com/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicekeycollection) 。 下面的代码示例演示如何通过名为 pKeyCollection 的变量向 [IPortableDeviceKeyCollection](https://docs.microsoft.com/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicekeycollection) 添加邮政编码数据字段。

```cpp
pKeyCollection->Add(SENSOR_DATA_TYPE_POSTALCODE);
```

## <a name="support-the-required-properties"></a>支持所需的属性

与其他传感器驱动程序一样，定位驱动程序通过一组属性提供有关传感器本身的信息。 Windows 硬件认证计划指定位置传感器必须支持的最低属性集。 有关传感器属性、其含义以及传感器驱动程序所需的属性的详细信息，请参阅 [**传感器属性**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-properties)。 下面的列表包含所需的属性：

- WPD \_ 功能 \_ 对象 \_ 类别

- 传感器 \_ 属性 \_ 类型

- 传感器 \_ 属性 \_ 状态

- 传感器 \_ 属性 \_ 持久 \_ 唯一 \_ ID

- 传感器 \_ 属性 \_ 制造商

- 传感器 \_ 属性 \_ 模型

- 传感器 \_ 属性 \_ 序列 \_ 号

- 传感器 \_ 属性 \_ 友好 \_ 名称

- 传感器 \_ 属性 \_ 最小 \_ 报表 \_ 间隔

- 传感器 \_ 属性 \_ 当前 \_ 报表 \_ 间隔

- 传感器 \_ 属性 \_ 位置 \_ 所需 \_ 准确性

## <a name="providing-data"></a>提供数据

位置驱动程序通过与其他传感器驱动程序相同的机制提供数据。 也就是说，传感器类扩展通过 [**ISensorDriver：： OnGetDataFields**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetdatafields) 调用驱动程序，驱动程序通过 *ppDataValues* 参数返回值。

以下要求适用于从位置传感器提供数据：

- 通过同步请求和通过 [引发事件](https://docs.microsoft.com/windows-hardware/drivers/sensors/raising-events)来提供数据。

- 维护最新数据报表的副本。 如果在你请求时新数据不可用，则返回缓存的报表。 不要更新时间戳。

- 不要为传感器 \_ 数据 \_ 类型的 \_ 纬度 \_ 度和传感器 \_ 数据 \_ 类型 \_ 经度度提供 \_ 超出现实世界纬度和经度的值。

- 不要报告值为 \_ \_ 零或小于零的传感器数据类型 \_ 错误 \_ RADIUS \_ 计量。

- 将传感器数据类型 "国家/地区" 的值设置 \_ \_ \_ \_ 为有效的 ISO 3166 1-2 国家/地区代码。

- 如果你的驱动程序支持纬度/经度和市政地址报告，则这些报告中的位置数据应对应于同一个物理位置。

下表描述了与 Location API 数据报表字段对应的传感器数据字段。 在为某个位置提供数据报表时使用这些数据字段常量。

| 传感器常量 | Location API 方法和属性 |
| --- | --- |
| SENSOR_DATA_TYPE_ADDRESS1 | [ICivicAddressReport::GetAddressLine1](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getaddressline1)<br><br>[LocationDisp. DispCivicAddressReport. AddressLine1](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-addressline1) |
| SENSOR_DATA_TYPE_ADDRESS2 | [ICivicAddressReport::GetAddressLine2](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getaddressline2)<br><br>[LocationDisp. DispCivicAddressReport. AddressLine2](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-addressline2) |
| SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_ERROR_METERS | [ILatLongReport::GetAltitudeError](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-getaltitudeerror)<br><br>[LocationDisp.DispLatLongReport.AltitudeError](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-altitudeerror) |
| SENSOR_DATA_TYPE_ALTITUDE_ELLIPSOID_METERS | [ILatLongReport::GetAltitude](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-getaltitude)<br><br>[LocationDisp. DispLatLongReport](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-altitude) |
| SENSOR_DATA_TYPE_CITY | [ICivicAddressReport::GetCity](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getcity)<br><br>[LocationDisp. DispCivicAddressReport](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-city)<br><br>[Windows. CivicAddress](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.CivicAddress#Windows_Devices_Geolocation_CivicAddress_City) |
| SENSOR_DATA_TYPE_COUNTRY_REGION | [ICivicAddressReport::GetCountryRegion](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getcountryregion)<br><br>[LocationDisp. DispCivicAddressReport](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-civicaddressreport-countryregion) |
| SENSOR_DATA_TYPE_ERROR_RADIUS_METERS | [ILatLongReport::GetErrorRadius](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-geterrorradius)<br><br>[LocationDisp.DispLatLongReport.ErrorRadius](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-errorradius) |
| SENSOR_DATA_TYPE_LATITUDE_DEGREES | [ILatLongReport::GetLatitude](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-getlatitude)<br><br>[LocationDisp. DispLatLongReport](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-latitude) |
| SENSOR_DATA_TYPE_LONGITUDE_DEGREES | [ILatLongReport::GetLongitude](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-ilatlongreport-getlongitude)<br><br>[LocationDisp. DispLatLongReport](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-displatlongreport-longitude) |
| SENSOR_DATA_TYPE_POSTALCODE | [ICivicAddressReport::GetPostalCode](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getpostalcode)<br><br>[LocationDisp. DispCivicAddressReport](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-postalcode) |
| SENSOR_DATA_TYPE_STATE_PROVINCE | [ICivicAddressReport::GetStateProvince](https://docs.microsoft.com/windows/win32/api/locationapi/nf-locationapi-icivicaddressreport-getstateprovince)<br><br>[LocationDisp. DispCivicAddressReport. StateProvince](https://docs.microsoft.com/windows/win32/locationapi/locationdisp-dispcivicaddressreport-stateprovince) |

## <a name="managing-state-transitions"></a>管理状态转换

传感器驱动程序可随时处于很多状态之一。 传感器状态由 [**SensorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001) 枚举定义。 若要正确使用 Location API，位置传感器必须遵循这些规则来处理状态转换。

- 始终在传感器 \_ 状态 \_ 初始化状态下启动，但在启动时不会引发状态更改事件。

- \_ \_ \_ \_ 当数据可用时，驱动程序应从传感器状态初始化转换为传感器状态 "就绪"。

- \_ \_ 当驱动程序没有当前要报告的数据时，驱动程序应转换回传感器状态初始化。 驱动程序应决定何时发生转换。 如果已丢失信号，但仍有方法提供有效数据，请保持传感器 \_ 状态 \_ 就绪状态。

- 始终按正确的顺序引发事件。 首先，确定数据可用。 然后引发状态更改事件。 最后，引发数据更新事件。

- 当驱动程序的状态发生更改时，始终引发状态更改事件。

-位置 API 不使用处于以下状态的传感器的数据：传感器 \_ 状态 " \_ 无 \_ 数据"、"传感器 \_ 状态 \_ \_ 不可用"、"传感器 \_ 状态错误" \_ 。

下表介绍了位置传感器驱动程序的各种传感器状态。

| 值 | 说明 | 位置 API 状态 |
| --- | --- | --- |
| SENSOR_STATE_READY | 传感器驱动程序可以提供具有完整且准确的数据的新位置报告。<br><br>例如，Wi-fi 或移动电话提供商已连接并且正常工作，或者 GPS 传感器有修补程序。<br><br>已使用三边转换传感器数据确定位置的 GPS 驱动程序处于此状态。 | REPORT_RUNNING |  
| SENSOR_STATE_INITIALIZING | 传感器驱动程序正在尝试获取修补程序。 传感器驱动程序应在修补程序被锁定并跟踪后将此状态转换为 SENSOR_STATE_READY。<br><br>例如，Wi-fi 提供商正在寻找 Internet 连接，移动电话提供商正在寻找无线电，或 GPS 传感器正在获取修补程序。<br><br>当 GPS 传感器尝试重新获取修复时，应重新进入此状态。 | REPORT_INITIALIZING |  
| SENSOR_STATE_NO_DATA | 位置提供程序可用，但无法提供位置数据。<br><br>例如，Wi-fi 提供程序有权访问 Internet，但该数据库没有位置数据。 | REPORT_ERROR |  
| SENSOR_STATE_NOT_AVAILABLE | 位置提供程序用于获取数据的功能被禁用。<br><br>如果无线电设备处于关闭状态，GPS 传感器会处于此状态。 | REPORT_ERROR |  
| SENSOR_STATE_ERROR | 传感器出现严重错误。 传感器可以从此状态恢复，但恢复的时间范围未知。 | REPORT_ERROR |  

下图显示了位置传感器中的状态转换。![状态转换](images/gps-state-transitions.png)

## <a name="raising-data-updated-and-state-changed-events"></a>引发数据更新和状态更改事件

Location API 需要位置传感器（如 GPS 传感器）来引发提供数据和状态更改信息的事件。 有关引发传感器事件的详细信息，请参阅 [关于传感器驱动程序事件](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-driver-events)。

引发这些事件时，位置驱动程序必须遵循以下规则：

- 通过调用传感器类扩展的 [**ISensorClassExtension：:P oststatechange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange) 方法引发状态更改事件。 不要调用 [**PostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent) 来引发状态更改事件。

- 通过调用 [**PostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)引发数据更新事件。

- 仅当数据是最新的且准确时才引发数据更新事件。

- 不要两次引发数据更新事件。 这意味着不应使用缓存数据引发数据更新事件。 您可以为响应数据的同步请求提供缓存数据。

- 通过事件发送纬度/经度报表时，始终包括所有必需的数据字段。

- 当传感器准确性变化时，始终引发数据更新事件。

- \_ \_ \_ \_ \_ 在引发事件或将传感器属性状态的值更改 \_ \_ 为传感器 \_ 状态 \_ 就绪之前，报告传感器数据类型错误 RADIUS 计量的有效值。

- 不要提供不完整的数据报告。

- 你可能没有所需的数据字段的当前数据，如 GPS 传感器丢失修补程序的时间。 在这种情况下，您可能仍希望提供有关扩展数据字段（如传感器 \_ 数据 \_ 类型 \_ NMEA 句子）更新的通知 \_ 。 若要提供此类通知，必须使用自定义事件类型并仅引发自定义事件，直到所需数据字段的数据可用。 有关如何定义自定义类型的信息，请参阅 [定义常量的自定义值](https://docs.microsoft.com/windows-hardware/drivers/sensors/defining-custom-values-for-constants)。

## <a name="related-topics"></a>相关主题

[电源和性能的位置驱动程序指南](location-driver-guidelines-for-power-and-performance.md)  
