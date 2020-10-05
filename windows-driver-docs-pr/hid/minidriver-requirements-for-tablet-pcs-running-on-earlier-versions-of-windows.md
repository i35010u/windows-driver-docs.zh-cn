---
title: 平板电脑的微型驱动程序要求
description: 介绍供应商提供的用于笔设备和按钮设备的 HID 微型驱动程序的一般要求。
ms.assetid: 89BE7E13-4D46-4265-9522-D5A51999F633
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b561ea83ff352272f9578d434a46700a1f819e12
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734399"
---
# <a name="minidriver-requirements-for-tablet-pcs-running-on-earlier-versions-of-windows"></a>在早期版本的 Windows 上运行的 tablet Pc 的微型驱动程序要求


本部分适用于 Windows 8 之前的操作系统，并介绍了供应商提供的适用于 tablet PC edition 系统上的笔设备和按钮设备的 HID 微型驱动程序的一般要求。

本部分重点介绍笔和按钮设备。

-   笔设备与 Tablet PC 的 LCD 显示器集成，用于捕获触笔的运动。
-   对笔设备进行了补充的按钮设备，用于捕获按钮输入。 有关 Tablet PC 的详细信息，请参阅 Windows XP Tablet PC Edition 网站

有关 Tablet PC 的详细信息，请参阅 [WINDOWS XP TABLET Pc Edition](/previous-versions/ms950406(v=msdn.10)) 网站。

有关系统提供的支持 Tablet PC 的软件的详细信息，请参阅 Microsoft Windows SDK 中的 Tablet PC 文档。

笔和按钮设备属于 HIDClass 设备安装程序类。 这些设备由系统提供的、连接到 HID 微型驱动程序的 [Hid 客户端驱动程序](hid-client-drivers.md)运行。 如果缺少支持设备硬件接口的系统提供的 HID 微型驱动程序，则需要供应商提供的 HID 微型驱动程序。 使用系统提供的 Tablet PC API 从用户模式操作设备，如 Windows SDK 文档中所述。

### <a name="requirements-for-pc-pen-devices"></a>PC 笔设备的要求

Tablet PC 笔设备必须：

-   提供 "使用情况" 页为数字化器，其使用情况为 "笔 (的顶级集合，请参阅 [HID 使用](hid-usages.md) 情况) 。

-   如果 Tablet pc 不包含内置的鼠标，则 Tablet PC 笔设备必须提供其使用情况页面为通用桌面并且其使用情况为鼠标的顶级集合。 鼠标集合的用途是启用系统鼠标光标。 但鼠标集合不能生成输入报告。 只应将来自笔集合的输入用于游标移动。  (如果 Tablet PC 的操作系统在没有安装的鼠标设备的情况下启动，则系统不会显示鼠标光标，也不会将笔集合作为鼠标设备处理。 ) 

-   仅报告原始数据。 驱动程序不得为线性、笔倾斜度、显示器旋转或缩放进行补偿。 这些转换由 Tablet PC API 处理。 但是，驱动程序必须确保钢笔坐标系统与 API 使用的源和方向相同。 例如，驱动程序必须确保源位于横向显示的左上角，x 坐标从左到右增加，以及 y 坐标从上到下增加了。

-   如果设备是 USB 设备，则 Tablet PC 笔设备必须支持 [USB 选择性挂起功能](/windows-hardware/drivers/ddi/index)。

### <a name="requirements-for-pc-button-devices"></a><a href="" id="ddk-requirements-on-hid-minidrivers-for-tablet-pc-button-devices-kg"></a>PC 按钮设备的要求

Tablet PC 按钮设备补充了 Tablet PC 上的笔输入。 按钮设备支持一个或多个按钮。 安装在 Tablet PC 上的按钮设备必须：

-   为安全注意序列提供一个专用按钮 (SAS)  (如 Microsoft Windows SDK 文档) 中所述。

-   按下按钮时生成事件，并在释放按钮时生成另一个事件。

-   每个按钮的报表不同按钮事件，而不考虑同时按下或释放的按钮数。

-   提供 "使用情况" 页为通用桌面并且其使用情况为键盘的顶级集合 (参阅 [HID 用法](hid-usages.md)) 。 键盘集合仅用于报告 SAS 按钮事件。 按下 SAS 按钮后，必须报告以下用法： "左"、"左 Alt" 和 "删除"。

-   提供 "使用情况" 页为通用桌面并且其使用情况为 Tablet PC 系统控件的顶级集合。 按钮事件的报告方法是使用 "使用情况" 页为 "button" 的按钮数组，使用值范围从1到按钮数目。

