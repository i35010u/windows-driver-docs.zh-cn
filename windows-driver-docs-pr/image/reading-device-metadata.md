---
title: 读取设备元数据
description: 读取设备元数据
ms.assetid: 402de9de-8bfe-4cc2-9b8e-06e0ad925eb1
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: cc45f14f2858c551c6393510d18bcd28bac3bb6f
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223561"
---
# <a name="reading-device-metadata"></a>读取设备元数据

WIA 微型驱动程序 for web 服务扫描程序必须在运行时读取以下设备元数据属性：

**PKEY \_ PNPX \_ ServiceId**

若要初始化[**WIA \_ DPS \_ 服务 \_ ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-service-id) WIA 属性，需要此属性。

**PKEY \_ PNPX \_ GlobalIdentity**

此属性初始化[**WIA \_ DPS \_ 全局 \_ 标识**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-global-identity)WIA 属性。

**PKEY \_ PNPX \_ ID**

此属性初始化[**WIA \_ DPS \_ 设备 \_ ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-device-id)设备属性。

> [!NOTE]
> 使用[ **IStiDeviceControl：： GetMyDevicePortName**直接或间接访问](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)

微型驱动程序还可以读取其他属性，包括以下属性：

**PKEY \_ PNPX \_ 固件 \_ 版本**

此属性初始化[**wia \_ DPA \_ 固件 \_ 版本**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-firmware-version)wia 属性。

> [!NOTE]
> 使用*WSDScan*的微型驱动程序也可以通过调用[**IStiDeviceControl：： GETMYDEVICEPORTNAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)检索 PNPX ID 值;返回的设备路径为当前 PKEY \_ PNPX \_ ID。

有关这些 PKEY \_ PNPX \_ *Xxx*属性的说明，请参阅[pnp-x 实施者指南](https://go.microsoft.com/fwlink/p/?linkid=242570)。

下面的代码示例演示如何为按上一部分所述获取的当前函数实例对象打开属性存储区，以及如何从存储区中读取设备属性：

[演示如何打开属性存储的代码示例](code-example-for-opening-a-property-store.md)

[演示如何读取设备属性的代码示例](code-example-for-reading-device-properties.md)

[演示如何初始化设备属性的代码示例](code-example-for-initializing-device-properties.md)
