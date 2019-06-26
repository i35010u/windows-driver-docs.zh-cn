---
Description: 对无线移动通信设备类的支持
title: 对无线移动通信设备类的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11052be367ecbb430fc218dfa52916bdfd6475df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358322"
---
# <a name="support-for-the-wireless-mobile-communication-device-class"></a>对无线移动通信设备类的支持


在 Windows Vista [USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)支持通用串行总线 (USB) 通信设备类 (CDC) 和 USB 无线移动通信设备类 （中包含的设备WMCDC)。

USB 无线移动通信设备类 (WMCDC) 规范建立连接、 控制和在主机和无线移动设备 （例如，移动电话） 之间的内容交换的标准时将设备连接到 USB 端口。 WMCDC 是通信设备类 (CDC)，其中包含各种通信和网络设备的扩展。 本部分介绍在 Windows 操作系统中支持 CDC 和 WMCDC 设备的体系结构。

WMCDC 设备包含的分组为多个函数*逻辑手机*。 大多数 WMCDC 设备都有单个逻辑手机，但设备可能有多个逻辑手机。 逻辑手机通常包括诸如数据/传真调制解调器、 对象存储事件和调用控制设备。 逻辑手机可能还包括支持 USB 音频类规范、 USB 人工输入设备 (HID) 类规范和 USB 视频类规范等其他 USB 规范定义的函数。

Windows WMCDC 体系结构使用本机 Windows 驱动程序来管理 WMCDC 设备的功能。 例如，可以使用 Windows 电话服务应用程序程序接口 (TAPI) 子系统来管理你的设备和 Windows 网络驱动程序接口规格 (NDIS) 子系统来管理设备的以太网的语音和数据/传真调制解调器函数LAN 函数。 此外，你可以管理一些函数，如一个对象交换协议 (OBEX) 函数，在用户模式软件中的帮助下[WinUSB](winusb.md) (Winusb.sys)。

下图显示了 WMCDC 设备的示例驱动程序堆栈。

![示例设备配置和驱动程序堆栈](images/wmcdc-architecture.png)

在上图中，WMCDC 设备包含单个逻辑话筒： OBEX 函数和调制解调器函数。 供应商提供的 INF 文件加载本机 Windows 驱动程序来管理调制解调器。 OBEX 函数由运行中的供应商提供的用户模式驱动程序[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/user-mode-driver-framework-design-guide)(UMDF)。 用户模式驱动程序使用 Windows 便携式设备 (WPD) 协议与用户应用程序和接口进行通信， [WinUSB](winusb.md)导出与 USB 堆栈进行通信。 一般情况下，供应商提供的 INF 文件将加载的每个接口集合使用 Winusb.sys Winusb.sys 的单独实例。

### <a name="registry-settings"></a>注册表设置

USB 堆栈不会自动支持 WMCDC。 必须提供加载 Usbccgp.sys 的实例的 INF 文件。 INF 文件必须包含**AddReg**设置部分**EnumeratorClass**到 REG Usbccgp.sys 与相关联的软件密钥中的注册表值\_二进制值。从三个数字构造：0x02，0x00，和 0x00。 示例 INF 文件从下面的代码示例演示了如何设置**EnumeratorClass**为适当的值。

```cpp
[CCGPDriverInstall.NT]
Include=usb.inf
Needs=Composite.Dev.NT
AddReg=CCGPDriverInstall.AddReg

[CCGPDriverInstall.NT.Services]
Include=usb.inf
Needs=Composite.Dev.NT.Services

[CCGPDriverInstall.AddReg]
HKR,,EnumeratorClass, 0x00000001,02,00,00
```

必须将分配给的值**EnumeratorClass**从 INF 文件中由对的十六进制数字表示的三个 1 字节二进制值构造：02、 00 和 00。 以下三个数字对应于 USB 实现论坛分配给 CDC 设备类、 CDC 设备子类和 CDC 设备协议，分别的值。

有关如何配置注册表，以正确地枚举 WMCDC 设备的详细信息，请参阅[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。

进一步的以下主题介绍 WMCDC:


## <a name="related-topics"></a>相关主题
[USB 泛型父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  



