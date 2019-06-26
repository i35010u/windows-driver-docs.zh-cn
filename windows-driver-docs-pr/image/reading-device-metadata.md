---
title: 读取设备元数据
description: 读取设备元数据
ms.assetid: 402de9de-8bfe-4cc2-9b8e-06e0ad925eb1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f159226170ede9a053dde1aa19d7f530fff1123
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374292"
---
# <a name="reading-device-metadata"></a>读取设备元数据


为 web services 扫描仪 WIA 微型驱动程序必须读取以下设备元数据属性在运行时：

<a href="" id="pkey-pnpx-serviceid"></a>**PKEY\_PNPX\_ServiceId**  
此属性需要初始化[ **WIA\_DPS\_服务\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-service-id) WIA 属性。

<a href="" id="pkey-pnpx-globalidentity"></a>**PKEY\_PNPX\_GlobalIdentity**  
此属性初始化[ **WIA\_DPS\_全局\_标识**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-global-identity) WIA 属性。

<a href="" id="pkey-pnpx-id--directly-or-indirectly-by-using-istidevicecontrol--getmydeviceportname-"></a>**主键\_PNPX\_ID** (直接或间接通过使用[ **IStiDeviceControl::GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname))  
此属性初始化[ **WIA\_DPS\_设备\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-device-id)设备属性。

微型驱动程序还可能读取其他属性，包括以下：

<a href="" id="pkey-pnpx-firmware-version"></a>**PKEY\_PNPX\_FIRMWARE\_VERSION**  
此属性初始化[ **WIA\_DPA\_固件\_版本**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-firmware-version) WIA 属性。

**请注意**  使用的微型驱动程序*WSDScan.sys*还可以通过调用检索 PNPX ID 值[ **IStiDeviceControl::GetMyDevicePortName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname);返回的设备路径是当前主键\_PNPX\_id。

 

有关说明这些主键\_PNPX\_*Xxx*属性，请参阅[PNP X 实施人员指南](https://go.microsoft.com/fwlink/p/?linkid=242570)。

下面的代码示例显示如何打开在上一部分中所述获取的当前函数实例对象的属性存储区以及如何从存储读取设备属性：

[用于打开属性存储的代码示例](code-example-for-opening-a-property-store.md)

[用于读取设备属性的代码示例](code-example-for-reading-device-properties.md)

[用于初始化设备属性的代码示例](code-example-for-initializing-device-properties.md)

 

 




