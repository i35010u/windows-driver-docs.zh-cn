---
title: 标准 USB 标识符
description: 标准 USB 标识符
ms.assetid: 39acb62b-83f2-4d14-a678-c37817193f01
keywords:
- USB 标识符 WDK 设备安装
- 单个接口 WDK USB 设备
- 多个接口 WDK USB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 278434ff8936d3ecd3067defc3d817ffd5aac922
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369407"
---
# <a name="standard-usb-identifiers"></a>标准 USB 标识符





<a href="" id="the-set-of-identifiers-generated-for-usb-devices-depends-on-whether-the-device-is-a-single-interface-device-or-a-multiple-interface-device-"></a>标识符为 USB 设备生成的集取决于设备是单个接口设备或多个接口设备。  

### <a name="single-interface-usb-devices"></a>单个接口 USB 设备

当在插入新的 USB 设备时，系统提供的 USB 集线器驱动程序通过使用设备的设备描述符从提取的信息来组合下列设备 ID:

USB\\VID_v(4)&PID_d(4)&REV_r(4)

其中：

-   *v(4)* 是 USB 委员会将分配给供应商的 4 位供应商代码。

-   *d(4)* 是供应商将分配给设备的 4 个数字的产品代码。

-   *r(4)* 是修订代码。

中心驱动程序提取从供应商和产品代码*idVendor*并*idProduct*设备描述符字段分别。

INF 模型部分还可以指定以下硬件 ID:

USB\\VID_v(4)&PID_d(4)

和以下兼容 Id:

USB\\CLASS_c(2)&SUBCLASS_s(2)&PROT_p(2)

USB\\CLASS_c(2)&SUBCLASS_s(2)

USB\\CLASS_c(2)

其中：

-   *c(2)* 是取自设备描述符的设备类代码。

-   *s(2)* 是设备子类代码。

-   *p(2)* 是协议代码。

设备类代码、 子类代码和协议代码由*bDeviceClass，bDeviceSubClass，* 并*bDeviceProtocol*设备描述符字段分别。 这些是两位数的数字。

### <a name="multiple-interface-usb-devices"></a>多个接口 USB 设备

设备具有多个接口称为*复合*设备。 从 Windows 2000 中，新建[USB 复合设备](https://msdn.microsoft.com/library/windows/hardware/ff537109)插入到一台计算机，USB 集线器驱动程序创建一个物理设备对象 (PDO)，并通知其的子设备集已更改的操作系统。 查询使用新的 PDO 相关联的硬件标识符的中心驱动程序后, 操作系统搜索相应的 INF 文件，查找匹配项的标识符。 如果它找到的匹配项以外*USB\\复合*，它会加载驱动程序 INF 文件中指定。 但是，如果不找到任何其他匹配项，则操作系统将使用兼容 ID *USB\\复合*，它将加载通用父表 USB 驱动程序。 泛型父驱动程序然后创建一个单独的 PDO，并生成一组单独的复合设备的每个接口的硬件标识符。

每个接口具有以下形式的设备 ID:

USB\\ VID_v(4)&PID_d(4)&MI_z(2)

其中：

-   *v(4)* 是 USB 委员会将分配给供应商的 4 位供应商代码。

-   *d(4)* 是供应商将分配给设备的 4 个数字的产品代码。

-   *z(2)* 是从提取接口编号*bInterfaceNumber*接口描述符字段。

INF 模型部分还可以指定以下兼容 Id:

USB\\CLASS_d(2)&SUBCLASS_s(2)&PROT_p(2)

USB\\CLASS_d(2)&SUBCLASS_s(2)

USB\\CLASS_d(2)

USB\\复合

其中：

-   *d(2)* 是取自设备描述符的设备类代码。

-   *s(2)* 是子类代码。

-   *p(2)* 是协议代码。

设备类代码、 子类代码和协议代码由*bInterfaceClass，bInterfaceSubClass，和 bInterfaceProtocol*接口描述符字段分别。 这些是两位数的数字。

 

 





