---
title: 低耗电蓝牙概述
description: 本部分提供了 Windows 8 中引入的蓝牙低能耗的概述
ms.assetid: 8783E31B-99A3-40EB-8A67-647AFAB7D4D3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 407eae063303e1cd8725bd55d4ce07889b32970d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391563"
---
# <a name="bluetooth-low-energy-overview"></a>低耗电蓝牙概述


Windows 8 引入了对蓝牙低功耗技术的支持。

蓝牙低能耗引入了新的物理层共享相同的频率空间蓝牙基本速率。 在这种技术开发的配置文件组织为泛型属性配置文件 （或 GATT）。

每个配置文件定义一个或多个服务，以创建用例或方案的使用。 符合标准的服务实现从组织方式与已建立蓝牙特别兴趣组上定义的架构一致的特征构造[开发人员网站](https://www.bluetooth.com/specifications/gatt/services/)。

下图显示了对象构建典型的 GATT 服务内的方式。

![蓝牙低功耗 gatt 服务声明](images/bthleservicedeclaration.png)

时与 Windows 8 计算机配对的蓝牙低能耗设备，设备会成为系统的一部分，并且 Windows 将提供设备对象来表示设备和设备报告的主服务。

![windows 8 蓝牙低功耗实现的设备对象结构](images/bthlewin8supt.png)

每个设备和其主服务表示为 Windows 中的设备对象和这些设备对象可查询和管理使用[设备安装函数](https://docs.microsoft.com/previous-versions/ff549791(v=vs.85))如[ **SetupDiEnumDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)，并[ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)。

除了标准[配置文件的蓝牙驱动程序函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，Windows 8 引入了新[蓝牙低能耗函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)允许使用蓝牙 GATT 客户端应用程序的开发。

这些函数允许服务和 （包括服务、 特征和其描述符） 及其对象的枚举，以及读取和写入功能。

 

 





