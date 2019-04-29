---
title: 读取设备元数据
description: 读取设备元数据
ms.assetid: 402de9de-8bfe-4cc2-9b8e-06e0ad925eb1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6b6a3e9a710c66073199cbd743df7325ccac19d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379614"
---
# <a name="reading-device-metadata"></a>读取设备元数据


为 web services 扫描仪 WIA 微型驱动程序必须读取以下设备元数据属性在运行时：

<a href="" id="pkey-pnpx-serviceid"></a>**PKEY\_PNPX\_ServiceId**  
此属性需要初始化[ **WIA\_DPS\_服务\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551428) WIA 属性。

<a href="" id="pkey-pnpx-globalidentity"></a>**PKEY\_PNPX\_GlobalIdentity**  
此属性初始化[ **WIA\_DPS\_全局\_标识**](https://msdn.microsoft.com/library/windows/hardware/ff551395) WIA 属性。

<a href="" id="pkey-pnpx-id--directly-or-indirectly-by-using-istidevicecontrol--getmydeviceportname-"></a>**主键\_PNPX\_ID** (直接或间接通过使用[ **IStiDeviceControl::GetMyDevicePortName**](https://msdn.microsoft.com/library/windows/hardware/ff542944))  
此属性初始化[ **WIA\_DPS\_设备\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551374)设备属性。

微型驱动程序还可能读取其他属性，包括以下：

<a href="" id="pkey-pnpx-firmware-version"></a>**PKEY\_PNPX\_FIRMWARE\_VERSION**  
此属性初始化[ **WIA\_DPA\_固件\_版本**](https://msdn.microsoft.com/library/windows/hardware/ff550309) WIA 属性。

**请注意**  使用的微型驱动程序*WSDScan.sys*还可以通过调用检索 PNPX ID 值[ **IStiDeviceControl::GetMyDevicePortName** ](https://msdn.microsoft.com/library/windows/hardware/ff542944);返回的设备路径是当前主键\_PNPX\_id。

 

有关说明这些主键\_PNPX\_*Xxx*属性，请参阅[PNP X 实施人员指南](https://go.microsoft.com/fwlink/p/?linkid=242570)。

下面的代码示例显示如何打开在上一部分中所述获取的当前函数实例对象的属性存储区以及如何从存储读取设备属性：

[用于打开属性存储的代码示例](code-example-for-opening-a-property-store.md)

[用于读取设备属性的代码示例](code-example-for-reading-device-properties.md)

[用于初始化设备属性的代码示例](code-example-for-initializing-device-properties.md)

 

 




