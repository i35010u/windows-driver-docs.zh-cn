---
title: 读取设备元数据
description: 读取设备元数据
ms.assetid: 402de9de-8bfe-4cc2-9b8e-06e0ad925eb1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca3fe282e179ca0ad3985194adcb1c6b577b651
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840765"
---
# <a name="reading-device-metadata"></a>读取设备元数据


WIA 微型驱动程序 for web 服务扫描程序必须在运行时读取以下设备元数据属性：

<a href="" id="pkey-pnpx-serviceid"></a>**PKEY\_PNPX\_ServiceId**  
需要此属性来初始化[**WIA\_DPS\_SERVICE\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-service-id) WIA 属性。

<a href="" id="pkey-pnpx-globalidentity"></a>**PKEY\_PNPX\_GlobalIdentity**  
此属性初始化[**WIA\_DPS\_GLOBAL\_IDENTITY**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-global-identity) WIA 属性。

<a href="" id="pkey-pnpx-id--directly-or-indirectly-by-using-istidevicecontrol--getmydeviceportname-"></a>**PKEY\_PNPX\_ID** （使用[**IStiDeviceControl：： GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)直接或间接）  
此属性初始化[**WIA\_dp\_设备\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-device-id)设备属性。

微型驱动程序还可以读取其他属性，包括以下属性：

<a href="" id="pkey-pnpx-firmware-version"></a>**PKEY\_PNPX\_固件\_版本**  
此属性初始化[**wia\_DPA\_固件\_版本**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-firmware-version)wia 属性。

**请注意**   使用*WSDScan*的微型驱动程序也可以通过调用[**IStiDeviceControl：： GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)来检索 PNPX ID 值;返回的设备路径为当前的 PKEY\_PNPX\_ID。

 

有关这些 PKEY\_PNPX\_*Xxx*属性的说明，请参阅[Pnp-x 实施者指南](https://go.microsoft.com/fwlink/p/?linkid=242570)。

下面的代码示例演示如何为按上一部分所述获取的当前函数实例对象打开属性存储区，以及如何从存储区中读取设备属性：

[用于打开属性存储的代码示例](code-example-for-opening-a-property-store.md)

[读取设备属性的代码示例](code-example-for-reading-device-properties.md)

[用于初始化设备属性的代码示例](code-example-for-initializing-device-properties.md)

 

 




