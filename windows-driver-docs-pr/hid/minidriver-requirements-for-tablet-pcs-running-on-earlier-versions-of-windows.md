---
title: 平板电脑的微型驱动程序要求
description: 描述供应商提供 HID 微型驱动程序笔和按钮的设备的常规要求。
ms.assetid: 89BE7E13-4D46-4265-9522-D5A51999F633
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9d506012ba8554a2bd9bd019ac69ad84cabc77f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566963"
---
# <a name="minidriver-requirements-for-tablet-pcs-running-on-earlier-versions-of-windows"></a>微型驱动程序要求 tablet Pc 更早版本的 Windows 上运行


本部分适用于 Windows 8 之前的操作系统，并描述供应商提供 HID 微型驱动程序笔和按钮在 tablet PC edition 系统安装的设备的常规要求。

本部分重点介绍笔和按钮的设备。

-   与 Tablet PC 集成笔设备的 LCD 显示器和用来捕获笔触笔的运动。
-   按钮设备是笔设备的补充，用于捕获按钮输入。 有关 Tablet PC 的详细信息，请参阅 Windows XP Tablet PC Edition 网站

有关 Tablet PC 的详细信息，请参阅[Windows XP Tablet PC Edition](https://go.microsoft.com/fwlink/p/?linkid=275069)网站。

有关支持 Tablet PC 的系统提供的软件的详细信息，请参阅 Microsoft Windows SDK 中的 Tablet PC 文档。

笔和按钮设备属于 HIDClass 设备安装程序类。 这些设备由系统提供运营[HID 客户端驱动程序](hid-client-drivers.md)，其链接到 HID 微型驱动程序。 如果没有系统提供 HID 微型驱动程序支持的设备的硬件接口，供应商提供 HID 微型驱动程序是必需的。 设备的操作是从用户模式下使用系统提供 Tablet PC API，这 Windows SDK 文档中所述。

### <a name="requirements-for-pc-pen-devices"></a>PC 笔设备的要求

Tablet PC 笔设备必须：

-   提供其使用情况该页是数字化器并且对其使用笔的顶级集合 (请参阅[HID 用法](hid-usages.md))。

-   如果 Tablet PC 不包括内置鼠标，Tablet PC 笔设备必须提供其使用情况页面是普通台式计算机和其用法是鼠标的顶级集合。 鼠标集合的目的是启用系统鼠标光标。 但是，鼠标集合必须不会生成输入的报表。 从笔集合的唯一输入应该用于光标的移动。 （如果不具有已安装的鼠标设备启动 Tablet PC 的操作系统，系统不会显示鼠标光标并不会处理作为鼠标设备的笔集合。）

-   仅限报表原始数据。 该驱动程序必须不补偿线性、 笔倾斜、 显示旋转或缩放。 这些转换由 Tablet PC API 处理。 但是，该驱动程序必须确保笔坐标系统使用相同的源和方向，与使用 api。 例如，原点位于横向显示的 x 坐标增加从左到右，左上角和 y 坐标增加从上到下，必须确保该驱动程序。

-   如果设备是 USB 设备、 Tablet PC 笔设备必须支持[USB 选择性挂起功能](https://msdn.microsoft.com/library/windows/hardware/ff540144)。

### <a href="" id="ddk-requirements-on-hid-minidrivers-for-tablet-pc-button-devices-kg"></a>PC 按钮设备的要求

Tablet PC 按钮设备对 Tablet PC 上的笔输入进行了补充。 按钮设备支持一个或多个按钮。 必须安装在 Tablet PC 的按钮设备：

-   提供一个专用的按钮的安全注意序列 (SAS) （如 Microsoft Windows SDK 文档中所述）。

-   生成按下某个按钮时发生的事件，另一个事件时释放该按钮。

-   报告每个按钮，无论包含几个按钮的同时按下或释放的非重复按钮事件。

-   提供其使用情况页面是普通台式计算机和其用法是键盘的顶级集合 (请参阅[HID 用法](hid-usages.md))。 键盘集合仅用于报告 SAS 按钮事件。 按下 SAS 按钮时，必须报告以下用法：左侧的控件左 alt 键，并删除。

-   提供其使用情况页面是普通台式计算机和其用法是 Tablet PC System Controls 的顶级集合。 通过使用其使用情况页面为按钮和使用情况的值的范围从 1 到按钮的数目的按钮数组报告按钮事件。

 

 




