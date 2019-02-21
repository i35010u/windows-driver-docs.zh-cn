---
title: HID 体系结构
description: Windows 中的 HID 驱动程序堆栈的体系结构是基于名为 hidclass.sys 类驱动程序。
ms.assetid: FCDDCD6A-8808-44D5-B300-3869DD9FD46C
keywords:
- HID 的类驱动程序
- hidclass.sys
- Windoows 的 HID 的类驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9f0ab4e1cbc32b693237557a749cec70a10ff92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522762"
---
# <a name="hid-architecture"></a>HID 体系结构


Windows 中的 HID 驱动程序堆栈的体系结构基于名为的类驱动程序*hidclass.sys*。 客户端和传输微型驱动程序从用户模式或内核模式下访问的类驱动程序。

## <a name="the-hid-class-driver"></a>HID 类驱动程序


在系统提供的 HID 类驱动程序是 WDM 功能驱动程序和总线驱动程序 HID 设备安装程序类 (HIDClass)。 HID 类驱动程序的可执行组件是*hidclass.sys*。 HID 类驱动程序是 HID 客户端和各种不同的传输在一起。 这允许隐藏客户端传输以独立方式编写。 此级别的抽象允许客户端可以继续使用 （很少或者不做任何修改） 时的新标准，或引入了第三方传输。

下面是体系结构的表示形式。 

![简化的 hid 驱动程序堆栈，显示隐藏客户端、 的 hid 的类驱动程序和 hid 的传输组件。](images/hid-intro-simple.png)

上图中包括以下组件：

-   HID 客户端 – 标识 Windows 和第三方客户端以及其接口。
-   HID 的类驱动程序- *hidclass.sys*可执行文件。
-   HID 的传输微型驱动程序的标识 Windows 和第三方传输和及其接口。

下面是泛型的 HID 客户端和传输的设备堆栈关系图。


![HID 的设备的通用 HID 客户端和传输堆栈。](images/hid-device-stacks-generic.png)

下面是另一个设备堆栈关系图显示通过 USB 的 HID 键盘和鼠标集合。

![使用键盘和鼠标悬停 USB HID 的设备堆栈。](images/hid-device-stacks.png)

## <a name="hid-clients"></a>HID 客户端


HID 客户端是驱动程序、 服务或应用程序与通信*HIDClass.sys*和通常表示特定类型的设备 （例如 传感器、 键盘、 鼠标等）。 它们标识通过硬件 ID 或特定的 HID 集合设备，并与以下指南通过 HID 集合进行通信。

用户模式驱动程序和应用程序和内核模式驱动程序，执行以下操作来操作 HID 集合：

-   用户模式驱动程序和应用程序使用 HIDClass 支持例程 (HidD\_Xxx) 以获取有关 HID 集合的信息。
-   内核模式驱动程序、 用户模式驱动程序和应用程序使用 HID 分析支持例程 (HidP\_Xxx)，和内核模式驱动程序使用 HID 类驱动程序 Ioctl 处理 HID 报告。

下表是信息的简化了上面列出。

|             | Drivers                      | 应用程序 |
|-------------|------------------------------|--------------|
| 用户模式   | HidD\_Xxx                    | HidP\_Xxx    |
| 内核模式 | HidD\_Xxx 或 IOCTL\_HID\_xxx | 不适用          |

 

有关详细信息，请参阅[打开 HID 集合](opening-hid-collections.md)。

有关所有受支持 HID 客户端的列表，请参阅[HID 支持在 Windows 中的客户端](hid-clients-supported-in-windows.md)。

## <a name="the-hid-transport-driver"></a>HID 传输驱动程序


HID 类驱动程序设计为使用 HID 微型驱动程序来访问硬件输入的设备。 HID 微型驱动程序对抽象，它支持的输入设备的特定于设备的操作。 HID 微型驱动程序的注册的 HID 类驱动程序将其操作绑定到的 HID 类驱动程序。 HID 类驱动程序通过调用微型驱动程序的支持例程与 HID 微型驱动程序进行通信。 HID 微型驱动程序，反过来，将关闭驱动程序堆栈的通信发送到基础总线或端口驱动程序。

在 Windows 中提供的 HID 传输的列表，请参阅[HID 传输方式在 Windows 中受支持](hid-transports-supported-in-windows.md)。

 

 




