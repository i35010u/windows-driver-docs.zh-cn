---
title: HID 体系结构
description: Windows 中的 HID 驱动程序堆栈的体系结构基于名为 hidclass.sys 的类驱动程序。
ms.assetid: FCDDCD6A-8808-44D5-B300-3869DD9FD46C
keywords:
- HID 类驱动程序
- hidclass.sys
- Windoows 的 HID 类驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2770dea62a760e60732cb5727bdfb62b89d23eeb
ms.sourcegitcommit: 74a8dc9ef1da03857dec5cab8d304e2869ba54a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90759938"
---
# <a name="hid-architecture"></a>HID 体系结构


Windows 中的 HID 驱动程序堆栈的体系结构基于名为 *hidclass.sys* 的类驱动程序。 客户端和传输微型驱动程序从用户模式或内核模式访问类驱动程序。

## <a name="the-hid-class-driver"></a>HID 类驱动程序


系统提供的 HID 类驱动程序为 HID 设备安装程序类 (HIDClass) 的 WDM 函数驱动程序和总线驱动程序。 *hidclass.sys*HID 类驱动程序的可执行组件。 HID 类驱动程序在 HID 客户端和各种传输之间粘附。 这允许以独立的方式写入 HID 客户端传输。 此级别的抽象使客户端可以继续工作， (在引入新的标准或第三方传输时，几乎不会) 修改。

下面是体系结构的表示形式。 

![简化的 hid 驱动程序堆栈，显示 hid 客户端、hid 类驱动程序和 hid 传输组件。](images/hid-intro-simple.png)

上图包含以下内容：

-   HID 客户端–标识 Windows 和第三方客户端及其接口。
-   HID 类驱动程序- *hidclass.sys* 可执行文件。
-   HID 传输微型驱动程序-标识 Windows 和第三方传输及其接口。

下面是通用 HID 客户端和传输的设备堆栈关系图。


![用于通用 HID 客户端和传输的 HID 设备堆栈。](images/hid-device-stacks-generic.png)

下面是另一个设备堆栈关系图，它显示了 USB 上的 HID 键盘和鼠标的集合。

![用于 USB 上的键盘和鼠标的 HID 设备堆栈。](images/hid-device-stacks.png)

## <a name="hid-clients"></a>HID 客户端


HID 客户端是与 *HIDClass.sys* 通信的驱动程序、服务或应用程序，通常表示特定类型的设备 (例如 传感器、键盘、鼠标等) 。 它们通过硬件 ID 或特定 HID 集合标识设备，并通过以下指南与 HID 集合通信。

用户模式驱动程序和应用程序，以及内核模式驱动程序，请执行以下操作来操作 HID 集合：

-   用户模式驱动程序和应用程序使用 HIDClass 支持例程 (HidD \_ Xxx) 获取有关 HID 集合的信息。
-   内核模式驱动程序、用户模式驱动程序和应用程序使用 (HidP Xxx) 的 HID 分析支持例程 \_ ，并且内核模式驱动程序使用 hid 类驱动程序 IOCTLs 来处理 hid 报表。

下表简化了上面列出的信息。

|      模式   | 驱动程序                      | 应用程序 |
|-------------|------------------------------|--------------|
| 用户模式   | HidD \_ Xxx                    | HidP \_ Xxx    |
| 内核模式 | HidD \_ XXX 或 IOCTL \_ HID \_ Xxx | 空值          |

 

有关详细信息，请参阅 [打开 HID 集合](opening-hid-collections.md)。

有关所有受支持的 HID 客户端的列表，请参阅 [Windows 中支持的 Hid 客户端](hid-clients-supported-in-windows.md)。

## <a name="the-hid-transport-driver"></a>HID 传输驱动程序


HID 类驱动程序设计为使用 HID 微型驱动程序来访问硬件输入设备。 HID 微型驱动程序对它所支持的输入设备的设备特定操作进行了抽象。 HID 微型驱动程序通过将其注册到 hid 类驱动程序，将其操作绑定到 hid 类驱动程序。 HID 类驱动程序通过调用微型驱动程序的支持例程与 HID 微型驱动程序通信。 然后，HID 微型驱动程序将与驱动程序堆栈之间的通信发送到基础总线或端口驱动程序。

有关 Windows 中提供的 HID 传输的列表，请参阅 [windows 中支持的 Hid 传输](hid-transports-supported-in-windows.md)。

 

 




