---
title: 读取设备元数据
description: 读取设备元数据
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: a33e30dfa352b32a0ff05608ede34f44d6f9fed6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839247"
---
# <a name="reading-device-metadata"></a>读取设备元数据

WIA 微型驱动程序 for web 服务扫描程序必须在运行时读取以下设备元数据属性：

**PKEY \_ PNPX \_ ServiceId**

若要初始化 [**WIA \_ DPS \_ 服务 \_ ID**](./wia-dps-service-id.md) WIA 属性，需要此属性。

**PKEY \_ PNPX \_ GlobalIdentity**

此属性初始化 [**WIA \_ DPS \_ 全局 \_ 标识**](./wia-dps-global-identity.md) WIA 属性。

**PKEY \_ PNPX \_ ID**

此属性初始化 [**WIA \_ DPS \_ 设备 \_ ID**](./wia-dps-device-id.md) 设备属性。

> [!NOTE]
> 使用 [ **IStiDeviceControl：： GetMyDevicePortName** 直接或间接访问](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)

微型驱动程序还可以读取其他属性，包括以下属性：

**PKEY \_ PNPX \_ 固件 \_ 版本**

此属性初始化 [**wia \_ DPA \_ 固件 \_ 版本**](./wia-dpa-firmware-version.md) wia 属性。

> [!NOTE]
> 使用 *WSDScan.sys* 的微型驱动程序还可以通过调用 [**IStiDeviceControl：： GETMYDEVICEPORTNAME**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)检索 PNPX ID 值;返回的设备路径为当前 PKEY \_ PNPX \_ ID。

有关这些 PKEY \_ PNPX \_ *Xxx* 属性的说明，请参阅 [ (DOC 下载) 的 pnp-x 实施者指南](https://go.microsoft.com/fwlink/p/?linkid=242570)。

下面的代码示例演示如何为按上一部分所述获取的当前函数实例对象打开属性存储区，以及如何从存储区中读取设备属性：

[演示如何打开属性存储的代码示例](code-example-for-opening-a-property-store.md)

[演示如何读取设备属性的代码示例](code-example-for-reading-device-properties.md)

[演示如何初始化设备属性的代码示例](code-example-for-initializing-device-properties.md)
