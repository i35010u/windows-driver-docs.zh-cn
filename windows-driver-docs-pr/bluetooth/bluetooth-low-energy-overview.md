---
title: 低耗电蓝牙概述
description: 本部分概述了 Windows 8 中引入的蓝牙低能耗
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c78189a13f218e9bd2d2aecfd5de21c06b3d067
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798583"
---
# <a name="bluetooth-low-energy-overview"></a>低耗电蓝牙概述


Windows 8 引入了对蓝牙低能耗技术的支持。

蓝牙低能耗引入了一个新的物理层，它与蓝牙基本速度共享相同的频率空间。 在此技术上开发的配置文件组织到一般属性配置文件中 (或 GATT) 。

每个配置文件定义使用一个或多个服务来创建用例或方案。 符合性服务实现是按照与在蓝牙特别兴趣组 [开发人员网站](https://www.bluetooth.com/specifications/gatt/services/)上定义的已建立架构一致的方式构造的。

下图说明了在典型的 GATT 服务内构造对象的方式。

![蓝牙低能耗 gatt 服务声明](images/bthleservicedeclaration.png)

当蓝牙低能耗设备与 Windows 8 计算机配对时，设备将成为系统的一部分，Windows 将提供设备对象来表示设备和设备报告的主要服务。

![windows 8 蓝牙低能耗实现的设备对象结构](images/bthlewin8supt.png)

每个设备及其主要服务在 Windows 中都表示为设备对象，可以使用 [**SetupDiEnumDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinfo)和 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)等 [设备安装功能](/previous-versions/ff549791(v=vs.85))来查询和管理这些设备对象。

除了标准的 [蓝牙配置文件驱动程序函数](/windows-hardware/drivers/ddi/index)外，Windows 8 还引入了新的 [蓝牙低能耗功能](/windows-hardware/drivers/ddi/index) ，可用于开发 bluetooth GATT 客户端应用程序。

这些函数可用于枚举服务及其对象 (包括服务、特征及其描述符) 以及读写功能。

 

