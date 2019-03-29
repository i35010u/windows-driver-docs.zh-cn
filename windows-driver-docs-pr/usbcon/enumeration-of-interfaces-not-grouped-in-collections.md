---
Description: Interfaces on a composite USB device can be grouped in collections or represent one USB function individually.
title: 枚举 USB 复合设备上的接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbf80573b7a1b02012e13216d1215a8bf6b90e30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565133"
---
# <a name="enumeration-of-interfaces-on-usb-composite-devices"></a>枚举 USB 复合设备上的接口


复合的 USB 设备上的接口可以在集合中分组或分别表示一个 USB 函数。 接口不是在集合中分组后，泛型父驱动程序创建的每个接口 PDO，并为每个 PDO 生成一组硬件 Id。

*设备 ID*有关 PDO 接口具有以下形式：

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

在这些 Id:

-   *v(4)* 是 USB 标准委员会将分配给供应商的四位数字表示供应商代码。
-   *p(4)* 是供应商将分配给设备的四位数字产品代码。
-   *z(2)* 是从提取接口编号**bInterfaceNumber**接口描述符字段。

泛型父驱动程序还会生成以下兼容 Id，通过使用接口描述符中的信息 ([**USB\_界面\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff540065)):

`USB\CLASS_d(2)&SUBCLASS_s(2)&PROT_p(2)`

`USB\CLASS_d(2)&SUBCLASS_s(2)`

`USB\CLASS_d(2)`

在这些 Id:

-   *d(2)* 该类的代码 (**bInterfaceClass**)
-   *s(2)* 是子类代码 (**bInterfaceSubClass**)
-   *p(2)* 是协议代码 (**bInterfaceProtocol**)

每个这些代码是一个四位数字。

## <a name="related-topics"></a>相关主题
[复合的 USB 设备上的接口集合的枚举](support-for-interface-collections.md)  
[USB 泛型父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



