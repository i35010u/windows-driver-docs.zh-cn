---
title: 蓝牙邻近感应配置文件
description: 邻近配置文件定义两个目的是允许设备检测其邻近的角色。
ms.assetid: 6BA67CA4-AAE4-4D01-97A4-65970704E7ED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37466465999a8bc5569f2bfb4d15d4a807214b34
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354046"
---
# <a name="bluetooth-proximity-profile"></a>蓝牙邻近感应配置文件


邻近配置文件定义两个目的是允许设备检测其邻近的角色。

将调用两个角色：

-   邻近报告器
-   邻近监视器

![角色关系](images/bthleproximityroles.png)

## <a name="span-idproximityreporterspanspan-idproximityreporterspanspan-idproximityreporterspanproximity-reporter"></a><span id="Proximity_Reporter"></span><span id="proximity_reporter"></span><span id="PROXIMITY_REPORTER"></span>邻近报告器


邻近报告器需要 GATT 服务器。

邻近报告器支持以下 GATT 服务：

-   链接丢失服务 （必需）
-   （可选） 的即时警报服务
-   Tx Power 服务 （可选）

## <a name="span-idproximitymonitorspanspan-idproximitymonitorspanspan-idproximitymonitorspanproximity-monitor"></a><span id="Proximity_Monitor"></span><span id="proximity_monitor"></span><span id="PROXIMITY_MONITOR"></span>邻近监视器


邻近监视器是 GATT 客户端。 它应创建并维护要计算的信号路径丢失的连接，连接到邻近报告器以及监视器无线电信号强度信息 （或 RSSI）。 如果可选"Tx Power 服务"邻近报告器上可用，它可以使用此附加信息来通过减去从 Tx 功率级别 RSSI 规范化 RSSI 值。

## <a name="span-idsupportforgattinwindows81spanspan-idsupportforgattinwindows81span-support-for-gatt-in-windows81"></a><span id="_support_for_gatt_in_windows_8.1"></span><span id="_SUPPORT_FOR_GATT_IN_WINDOWS_8.1"></span> 对 Windows 8.1 中 GATT 的支持


时与 Windows 8.1 配对 GATT 设备，设备会成为系统的一部分，并且 Windows 将提供*设备对象*来表示设备和设备报告的主服务。

[ **Windows.Devices.Bluetooth.GenericAttributeProfile 命名空间**](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile)。 介绍了应用程序开发人员可以在 Windows 8.1 中使用的泛型属性配置文件 Api。

当开发设备应用程序的第一个步骤之一是确定的蓝牙服务应用程序需求，以便完成用户关心的方案。 邻近配置文件中，设备应用程序需要使用"链接丢失服务"并选择"即时警报服务"和"Tx Power 服务"。

为了使设备应用，以确定是否任何设备与配对的 Windows 实现"链接丢失服务"应用程序应使用中提供的 Api [ **Windows.Devices.Enumeration 命名空间**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)，即 DeviceInformation.FindAllAsync 方法。

[ **DeviceInformation.FindAllAsync 方法**](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_FindAllAsync_System_String_)采用*AQS （高级的查询语法）* 作为参数以筛选仅包含设备的设备选择器"链接丢失服务"。 设备应用程序开发人员还可以使用[ **GetDeviceSelectorFromUuid** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService#Windows_Devices_Bluetooth_GenericAttributeProfile_GattDeviceService_GetDeviceSelectorFromUuid_System_Guid_)或[ **GetDeviceSelectorFromShortId** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService#Windows_Devices_Bluetooth_GenericAttributeProfile_GattDeviceService_GetDeviceSelectorFromShortId_System_UInt16_) 方法[**GattDeviceService** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService)类，因此它们无需手动构造 AQS 筛选器。

"链接丢失服务"是由蓝牙 SIG，以及这种情况下定义的蓝牙 GATT 服务*短 Id*可用而不是*完全限定的 UUID*。

*短 Id*分配邻近配置文件服务的服务 Id 是：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">服务名称</th>
<th align="left">短 Id</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>链接丢失</p></td>
<td align="left"><p>0x1803</p></td>
</tr>
<tr class="even">
<td align="left"><p>即时警报</p></td>
<td align="left"><p>0x1802</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Tx 电源</p></td>
<td align="left"><p>0x1804</p></td>
</tr>
</tbody>
</table>

 

蓝牙 SIG 维护的最新[的服务列表](https://go.microsoft.com/fwlink/p/?linkid=320723)。

开发人员已确定哪个服务后他/她想要使用，他/她可以调用[ **GattDeviceService.FromIdAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService#Windows_Devices_Bluetooth_GenericAttributeProfile_GattDeviceService_FromIdAsync_System_String_)以获取服务的实例。

一旦开发人员已获取有效的 GattDeviceService 对象，他/她可以使用它来与设备使用通信[ **Windows.Devices.Bluetooth.GenericAttributeProfile** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile) API。

这些 Api 启用对特定的服务和它们的对象 （例如包含服务、 特征和描述符） 的访问，以及读取和写入功能。

[蓝牙泛型属性配置文件-心率服务](https://go.microsoft.com/fwlink/p/?linkid=301978)示例演示了其中一些技巧。

## <a name="span-idusingpowerefficientlyspanspan-idusingpowerefficientlyspanspan-idusingpowerefficientlyspanusing-power-efficiently"></a><span id="Using_Power_Efficiently"></span><span id="using_power_efficiently"></span><span id="USING_POWER_EFFICIENTLY"></span>有效地使用 Power


支持 Windows 8.1 的蓝牙低能耗具有有效地使用电源的重点。 这包括减少本地 Bluetooth 无线电适配器的功率消耗，以及使用 CPU 为尽可能少。

因此，若要建立蓝牙 LE 连接应用程序需要注册的处理程序[ **GattCharacteristic.ValueChanged** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_ValueChanged)事件。 或者，应用必须调用的任何[ **GattCharacteristic.ReadValueAsync**](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_ReadValueAsync_Windows_Devices_Bluetooth_BluetoothCacheMode_)， [ **GattCharacteristic.WriteValueAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_WriteValueAsync_Windows_Storage_Streams_IBuffer_)或[ **GattCharacteristic.WriteClientCharacteristicConfigurationDescriptorAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_WriteClientCharacteristicConfigurationDescriptorAsync_Windows_Devices_Bluetooth_GenericAttributeProfile_GattClientCharacteristicConfigurationDescriptorValue_)方法，而不必指定 BluetoothCacheMode.Cached 选项。

**请注意**  以尽可能减少能耗，Windows 不会主动监视链接 RSSI 值通过轮询本地蓝牙单选控制器。

 

说明了 power 注意事项[邻近配置文件实现细节](proximity-profile-implementation-details.md)。

 

 





