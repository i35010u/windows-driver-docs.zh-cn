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
ms.openlocfilehash: aec6baa54a113d686c8b10f671671d1985711940
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92356039"
---
# <a name="hid-architecture"></a>HID 体系结构

Windows 中的 HID 驱动程序堆栈的体系结构基于名为 *hidclass.sys* 的类驱动程序。 客户端和传输微型驱动程序从用户模式或内核模式访问类驱动程序。

## <a name="the-hid-class-driver"></a>HID 类驱动程序

系统提供的 HID 类驱动程序为 HID 设备安装程序类 (HIDClass) 的 WDM 函数驱动程序和总线驱动程序。 *hidclass.sys*HID 类驱动程序的可执行组件。 HID 类驱动程序在 HID 客户端和各种传输之间粘附。 这允许以独立的方式写入 HID 客户端传输。 此级别的抽象使客户端可以继续工作， (在引入新的标准或第三方传输时，几乎不会) 修改。

下面是体系结构的表示形式。

![简化的 hid 驱动程序堆栈，显示 hid 客户端、hid 类驱动程序和 hid 传输组件。](images/hid-intro-simple.png)

上图包含以下内容：

- HID 客户端–标识 Windows 和第三方客户端及其接口。
- HID 类驱动程序- *hidclass.sys* 可执行文件。
- HID 传输微型驱动程序-标识 Windows 和第三方传输及其接口。

下面是通用 HID 客户端和传输的设备堆栈关系图。

![用于通用 HID 客户端和传输的 HID 设备堆栈。](images/hid-device-stacks-generic.png)

下面是另一个设备堆栈关系图，它显示了 USB 上的 HID 键盘和鼠标的集合。

![用于 USB 上的键盘和鼠标的 HID 设备堆栈。](images/hid-device-stacks.png)

## <a name="hid-clients"></a>HID 客户端

HID 客户端是与 *HIDClass.sys* 通信的驱动程序、服务或应用程序，通常表示特定类型的设备 (例如 传感器、键盘、鼠标等) 。 它们通过硬件 ID 或特定 HID 集合标识设备，并通过以下指南与 HID 集合通信。

用户模式驱动程序和应用程序，以及内核模式驱动程序，请执行以下操作来操作 HID 集合：

- 用户模式驱动程序和应用程序使用 HIDClass 支持例程 (HidD \_ Xxx) 获取有关 HID 集合的信息。
- 内核模式驱动程序、用户模式驱动程序和应用程序使用 (HidP Xxx) 的 HID 分析支持例程 \_ ，并且内核模式驱动程序使用 hid 类驱动程序 IOCTLs 来处理 hid 报表。

下表简化了上面列出的信息。

|      “模式”   | 驱动程序                      | 应用程序 |
|-------------|------------------------------|--------------|
| 用户模式   | HidD \_ Xxx                    | HidP \_ Xxx    |
| 内核模式 | HidD \_ XXX 或 IOCTL \_ HID \_ Xxx | 不适用          |

有关详细信息，请参阅 [打开 HID 集合](opening-hid-collections.md)。

### <a name="hid-clients-supported-in-windows"></a>Windows 中支持的 HID 客户端

Windows 支持以下顶级集合：

| **使用情况页** | **使用情况** | **Windows 7** | **Windows 8** | **Windows 10** | **备注** | **访问模式** |
| --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | 0x0001-0x0002 | 是 | 是 | 是 | 鼠标类驱动程序和映射器驱动程序 | 排他 |
| 0x0001 | 0x0004 - 0x0005 | 是 | 是 | 是 | 游戏控制器 | 共享 |
| 0x0001 | 0x0006 - 0x0007 | 是 | 是 | 是 | 键盘/键盘类驱动程序和映射器驱动程序 | 排他 |
| 0x0001 | 0x000C | 否 | 是 | 是 | 飞行模式开关 | 共享 |
| 0x0001 | 0x0080 | 是 | 是 | 是 | 系统控件 (Power)  | 共享 |
| 0x000C | 0x0001 | 是 | 是 | 对于 Windows 10 和 Windows 10 移动版) 为 "是" ( | 使用者控件 | 适用于 Windows 10 和 Windows 10 移动版) 的共享 ( |
| 0x000D | 0x0001 | 是 | 是 | 是 | 外部笔设备 | 排他 |
| 0x000D | 0x0002 | 是 | 是 | 是 | 集成笔设备 | 排他 |
| 0x000D | 0x0004 | 是 | 是 | 是 | 触摸屏 | 排他 |
| 0x000D | 0x0005 | 否 | 是 | 是 | 精确的触摸板 (PTP)  | 排他 |
| 0x0020 | * 多个 | 否 | 是 | 是 | 传感器 | 共享 |
| 0x0084 | 0x004 | 是 | 是 | 是 | HID UPS 电池 | 共享 |
| 0x008C | 0x0002 | 否 | 是 (Windows 8.1 和更高版本)  | 是 | 条形码扫描器 ( # A0)  | 共享 |

在上表中，输入 HID 客户端的访问模式是独占的，以防止其他 HID 客户端在不是该输入的目标接收方时截获或接收全局输入状态。 因此，出于安全原因，边缘 (原始输入管理器) 会以独占方式打开所有此类设备。

共享模式允许多个应用程序访问设备。 例如，多个应用程序可以访问条形码扫描器来查询设备功能和检索统计信息。 但是，从条形码扫描程序中检索已解码的数据在独占模式下完成。 用法由 [USB IF 使用情况表](https://usb.org/document-library/hid-usage-tables-121)定义。

* 多：从0x00 –0xFF 的传感器使用情况出于不同目的进行分段。 例如，0x10 表示生物识别传感器;0x40 指示光传感器。 这些分配不是连续的。 有关传感器使用情况的列表，请参阅  [USB-IF Device Class Defnitions FOR HID](https://www.usb.org/document-library/device-class-definition-hid-111)。 有关 Windows 中支持的传感器使用情况的信息，请 [使用 HID 传感器](/windows-hardware/design/whitepapers/hid-sensors-usages)。

## <a name="the-hid-transport-driver"></a>HID 传输驱动程序

HID 类驱动程序设计为使用 HID 微型驱动程序来访问硬件输入设备。 HID 微型驱动程序对它所支持的输入设备的设备特定操作进行了抽象。 HID 微型驱动程序通过将其注册到 hid 类驱动程序，将其操作绑定到 hid 类驱动程序。 HID 类驱动程序通过调用微型驱动程序的支持例程与 HID 微型驱动程序通信。 然后，HID 微型驱动程序将与驱动程序堆栈之间的通信发送到基础总线或端口驱动程序。

### <a name="hid-transports-supported-in-windows"></a>Windows 中支持的 HID 传输方式

Windows 支持以下传输方式。

| Transport    | Windows 7 | Windows 8 | 注释                                                                                                 |
|--------------|-----------|-----------|-------------------------------------------------------------------------------------------------------|
| USB          | 是       | 是       | Windows 操作系统2000可追溯上提供了对 USB HID 1.11 + 的支持。       |
| Bluetooth    | 是       | 是       | Windows 操作系统可追溯上提供对蓝牙 HID 1.1 + 的支持。 |
| 蓝牙 LE | 否        | 是       | Windows 8 引入了对基于蓝牙 LE 的 HID 的支持。                                               |
| I2C          | 否        | 是       | Windows 8 通过 I2C 引入了对 HID 的支持                                                         |

Windows 7 之前的 Windows (早期版本) 还包括对以下项的支持。

- HidGame.sys-HID 微型驱动程序 for 游戏端口 (i/o 端口 201) 设备。 HID 类驱动程序为游戏端口设备创建一个功能设备对象 (FDO) ，并为游戏端口设备支持的每个 HID 集合创建 (PDO) 的物理设备对象。
- Gameenum.sys –游戏端口总线驱动程序。 游戏端口总线驱动程序为每个与游戏端口建立菊花链式的游戏端口设备创建一个 PDO。

它们现在被视为旧版，因为在新式计算机上找不到硬件 (替换为 USB 和其他新式传输) 。

## <a name="recommended-transports-for-keyboards-mice-and-touchpads"></a>建议用于键盘、鼠标和触摸板的传输

下表显示了适用于便携式) 计算机上的键盘、鼠标和触摸板设备的建议传输 (例如， (如 "一体" 和 "台式机) " 之类的非便携式系统。

| 系统类型                  | 可移植                                 | 不可移植                                |
|------------------------------|------------------------------------------|---------------------------------------------|
| 旧系统               | 内部： PS/2，外部： USB，蓝牙 | 内部：不适用，外部： USB，蓝牙     |
| 芯片上的系统 (SoC) 系统 | 内部： I2C，External： USB，蓝牙  | 内部： I2C，USB External： USB，蓝牙 |

Windows 硬件实验室工具包中的[**USB 一般 HID 测试**](/windows-hardware/test/hlk/testref/f7949ab5-dd13-4c74-876f-6d54ff85e213) (的 HLK) 包含 HidUsb 和 HidClass 驱动程序。 没有适用于第三方 HID 小型驱动程序的 HLK 测试。
