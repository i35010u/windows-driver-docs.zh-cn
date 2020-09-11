---
title: 蓝牙邻近感应配置文件
description: 邻近配置文件定义了两个角色，旨在允许设备检测其邻近性。
ms.assetid: 6BA67CA4-AAE4-4D01-97A4-65970704E7ED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2bbf1a7c65df3f94857aadd3e51460e4d796f7b
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009917"
---
# <a name="bluetooth-proximity-profile"></a>蓝牙邻近感应配置文件


邻近配置文件定义了两个角色，旨在允许设备检测其邻近性。

这两个角色被称为：

-   邻近报告器
-   邻近感应监视器

![角色关系](images/bthleproximityroles.png)

## <a name="span-idproximity_reporterspanspan-idproximity_reporterspanspan-idproximity_reporterspanproximity-reporter"></a><span id="Proximity_Reporter"></span><span id="proximity_reporter"></span><span id="PROXIMITY_REPORTER"></span>邻近报告器


邻近报表需要是 GATT 服务器。

邻近报告器支持以下 GATT 服务：

-   链接丢失服务 (必需的) 
-   即时警报服务 (可选) 
-   Tx Power Service (可选) 

## <a name="span-idproximity_monitorspanspan-idproximity_monitorspanspan-idproximity_monitorspanproximity-monitor"></a><span id="Proximity_Monitor"></span><span id="proximity_monitor"></span><span id="PROXIMITY_MONITOR"></span>邻近性监视器


邻近感应监视器是 GATT 客户端。 它应该创建并维护与邻近报告器的连接，并监视连接 (或 RSSI) 的无线电信号强度信息，以计算信号的路径丢失。 如果邻近报告器中提供了可选的 "Tx Power Service"，则它还可以使用此附加信息来规范化 RSSI 值，方法是将 RSSI 从 Tx 电源级别减去。

## <a name="span-id_support_for_gatt_in_windows_81spanspan-id_support_for_gatt_in_windows_81span-support-for-gatt-in-windows81"></a><span id="_support_for_gatt_in_windows_8.1"></span><span id="_SUPPORT_FOR_GATT_IN_WINDOWS_8.1"></span> Windows 8.1 中的 GATT 支持


当 GATT 设备与 Windows 8.1 配对时，设备将成为系统的一部分，Windows 将提供 *设备对象* 以表示设备和设备报告的主要服务。

[**Bluetooth.genericattributeprofile 替换命名空间**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile)。 介绍一般属性配置文件 Api 应用开发人员可在 Windows 8.1 中使用。

开发设备应用程序的第一步是确定应用程序需要哪些蓝牙服务才能完成用户所关心的方案。 对于邻近配置文件，设备应用需要使用 "链接丢失服务" 以及（可选） "即时警报服务" 和 "Tx Power Service"。

为了使设备应用程序能够确定与 Windows 配对的任何设备是否实现了 "链接丢失服务"，应用应使用 [**Windows**](/uwp/api/Windows.Devices.Enumeration)中提供的 api，即 DeviceInformation. FindAllAsync 方法。

[**DeviceInformation. FindAllAsync 方法**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation#Windows_Devices_Enumeration_DeviceInformation_FindAllAsync_System_String_)采用*AQS (高级查询语法) *设备选择器作为参数，以便仅筛选包含 "链接丢失服务" 的设备。 设备应用开发人员还可以使用[**GattDeviceService**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService)类的[**GetDeviceSelectorFromUuid**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService#Windows_Devices_Bluetooth_GenericAttributeProfile_GattDeviceService_GetDeviceSelectorFromUuid_System_Guid_)或[**GetDeviceSelectorFromShortId**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService#Windows_Devices_Bluetooth_GenericAttributeProfile_GattDeviceService_GetDeviceSelectorFromShortId_System_UInt16_)方法，因此它们不需要手动构造 AQS 筛选器。

"链接丢失服务" 是由蓝牙 SIG 定义的蓝牙 GATT 服务，因此可以使用这种 *短 Id* ，而不是 *完全限定的 UUID*。

为邻近配置文件服务分配的 *短 id* 服务 id 为：

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
<td align="left"><p>Tx 幂</p></td>
<td align="left"><p>0x1804</p></td>
</tr>
</tbody>
</table>

 

蓝牙 SIG 维护服务的最新 [列表](https://go.microsoft.com/fwlink/p/?linkid=320723)。

开发人员确定了要使用的服务后，s/她可以调用 [**GattDeviceService**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattDeviceService#Windows_Devices_Bluetooth_GenericAttributeProfile_GattDeviceService_FromIdAsync_System_String_) 来获取服务的实例。

开发人员获得有效的 GattDeviceService 对象后，s/她就可以使用 [**Bluetooth.genericattributeprofile 替换**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile) API 与设备进行通信。

使用这些 Api 可以访问特定服务及其对象 (例如包括的服务、特征和描述符) ，以及读写功能。

[蓝牙通用属性配置文件-心率服务](https://go.microsoft.com/fwlink/p/?linkid=301978)示例演示了其中的一些方法。

## <a name="span-idusing_power_efficientlyspanspan-idusing_power_efficientlyspanspan-idusing_power_efficientlyspanusing-power-efficiently"></a><span id="Using_Power_Efficiently"></span><span id="using_power_efficiently"></span><span id="USING_POWER_EFFICIENTLY"></span>有效使用电源


在 Windows 8.1 中对蓝牙低能耗的支持具有有效地使用电源的强大功能。 这包括降低本地蓝牙无线电适配器的能耗，并尽可能少地使用 CPU。

因此，若要建立蓝牙 LE 连接，应用需要为 [**GattCharacteristic. ValueChanged**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_ValueChanged) 事件注册处理程序。 或者，应用程序必须调用 [**GattCharacteristic、ReadValueAsync**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_ReadValueAsync_Windows_Devices_Bluetooth_BluetoothCacheMode_)、 [**GattCharacteristic**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_WriteValueAsync_Windows_Storage_Streams_IBuffer_) [**或 GattCharacteristic**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattCharacteristic#Windows_Devices_Bluetooth_GenericAttributeProfile_GattCharacteristic_WriteClientCharacteristicConfigurationDescriptorAsync_Windows_Devices_Bluetooth_GenericAttributeProfile_GattClientCharacteristicConfigurationDescriptorValue_) 方法中的任何一个，而无需指定 WriteClientCharacteristicConfigurationDescriptorAsync 选项。

**注意**   为了最大限度地减少能耗，Windows 不会通过轮询本地蓝牙无线电控制器主动监视链接的 RSSI 值。

 

有关电源注意事项的详细信息，请参阅 [邻近分析实现细节](proximity-profile-implementation-details.md)。

 

