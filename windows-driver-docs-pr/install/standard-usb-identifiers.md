---
title: 标准 USB 标识符
description: 标准 USB 标识符
keywords:
- USB 标识符 WDK 设备安装
- 单接口设备 WDK USB
- 多接口设备 WDK USB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58446bee48c4d12cb0c8c6228e9184c59e21614c
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124161"
---
# <a name="standard-usb-identifiers"></a>标准 USB 标识符





<a href="" id="the-set-of-identifiers-generated-for-usb-devices-depends-on-whether-the-device-is-a-single-interface-device-or-a-multiple-interface-device-"></a>为 USB 设备生成的标识符集取决于设备是单接口设备还是多接口设备。  

### <a name="single-interface-usb-devices"></a>Single-Interface USB 设备

插入新的 USB 设备时，系统提供的 USB 集线器驱动程序将使用从设备的设备描述符中提取的信息来撰写以下设备 ID：

USB \\ VID_v (4) # B0 PID_d (4) # B1 REV_r (4) 

其中：

-   *(4)* 是 USB 委员会分配给供应商的4位数供应商代码。

-   *d (4)* 是供应商分配给设备的4位数产品代码。

-   *r (4)* 是版本代码。

集线器驱动程序分别从设备描述符的 *idVendor* 和 *idProduct* 字段中提取供应商和产品代码。

INF 模型部分还可以指定以下硬件 ID：

USB \\ VID_v (4) # B0 PID_d (4) 

和以下兼容 Id：

USB \\ CLASS_c (2) # B0 SUBCLASS_s (2) # B1 PROT_p (2) 

USB \\ CLASS_c (2) # B0 SUBCLASS_s (2) 

USB \\ CLASS_c (2) 

其中：

-   *c (2)* 是从设备描述符获取的设备类代码。

-   *s (2)* 是设备子类代码。

-   *p (2)* 为协议代码。

设备类代码、子类代码和协议代码分别由设备描述符的 *bDeviceClass、bDeviceSubClass* 和 *bDeviceProtocol* 字段决定。 它们是2位数字。

### <a name="multiple-interface-usb-devices"></a>Multiple-Interface USB 设备

具有多个接口的设备称为 *复合* 设备。 从 Windows 2000 开始，当将新的 [USB 复合设备](../usbcon/register-a-composite-driver.md) 插入计算机时，usb 集线器驱动程序将 (PDO 创建物理设备对象) 并通知操作系统其子设备集已更改。 查询用于与新 PDO 关联的硬件标识符的集线器驱动程序后，操作系统会搜索相应的 INF 文件以查找标识符的匹配项。 如果找到除 *USB \\ 复合* 以外的匹配项，它将加载 INF 文件中指示的驱动程序。 但是，如果未找到任何其他匹配项，则操作系统将使用兼容的 ID *usb \\ 复合*，它将加载 usb 通用父驱动程序。 然后，一般父驱动程序创建一个单独的 PDO，并为复合设备的每个接口生成一组单独的硬件标识符。

每个接口都具有以下形式的设备 ID：

USB \\ VID_v (4) # B0 PID_d (4) # B1 MI_z (2) 

其中：

-   *(4)* 是 USB 委员会分配给供应商的4位数供应商代码。

-   *d (4)* 是供应商分配给设备的4位数产品代码。

-   *z (2)* 是从接口描述符的 *bInterfaceNumber* 字段中提取的接口号。

INF 模型部分还可以指定以下兼容 Id：

USB \\ CLASS_d (2) # B0 SUBCLASS_s (2) # B1 PROT_p (2) 

USB \\ CLASS_d (2) # B0 SUBCLASS_s (2) 

USB \\ CLASS_d (2) 

USB \\ 复合

其中：

-   *d (2)* 是从设备描述符获取的设备类代码。

-   *s (2)* 为子类代码。

-   *p (2)* 为协议代码。

设备类代码、子类代码和协议代码分别由接口描述符中的 *bInterfaceClass、bInterfaceSubClass 和 bInterfaceProtocol* 字段决定。 它们是2位数字。

