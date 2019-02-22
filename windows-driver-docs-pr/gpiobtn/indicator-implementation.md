---
title: 指示器实现
description: 本主题介绍指示器实现。
ms.assetid: 60BCE8C7-416E-4D5B-9B32-9B398CEA6A8A
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8c8774c64672b171c9e8e1825a0ce60ebdb1c5d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554906"
---
# <a name="indicator-implementation"></a>指示器实现

本主题介绍指示器实现。

因为传感器位置和相关的逻辑因系统而异，务必要更新的模式时系统执行所有相关的 power 过渡，如下所示：

- 来自连接待机
- 带即将进入睡眠或休眠状态
- 启动后

这强制实施正确的状态，并确保刷新到用户界面层。

## <a name="laptopslate-mode---implementation-for-convertibles"></a>便携式计算机/盖板模式-实现双用型

*图 1 可转换为实现选项*显示转换的系统上实现 GPIO 指示器的选项。

![转换实现选项](images/implementationconvertibles.jpg)

图 1 转换实现选项

## <a name="laptopslate-mode---implementation-for-laptops"></a>便携式计算机/盖板模式-实现的便携式计算机

*图 2 便携式计算机实现选项*显示了用于实现 GPIO 指示器的便携式计算机系统上的选项。

![便携式计算机实现选项](images/implementationlaptops.jpg)

图 2 便携式计算机实现选项

ConvertibleSlateMode[无人参与 Windows 安装程序](https://go.microsoft.com/fwlink/p/?linkid=276788)设置允许 Oem 到便携式计算机模式下的静态标志闭合包装到作为映像自定义而无需实现注入机制。

此功能面向具有永久附加的键盘 （它用户可以在任何时候使用） 的触摸屏系统。 下面已没有 GPIO 指示器的触摸屏蛤所提供的示例 / 注入可用。

此设置必须应用专用的配置阶段的一部分，并且可以应用于所有 Windows 客户端操作系统。 请参阅[标识无人参与设置传递](http://sharepoint/sites/cba/Wiki Pages/Identifying Unattend Setting Passes.aspx)有关详细信息。

代码示例，请参阅。

> [!NOTE]
> - GPIO 按钮驱动程序加载重写中引入了无人参与设置的值。
> - 可与 Windows 8.1 系统注入机制。
> - ConvertibleSlateMode 无人参与设置不影响 Windows 8 到 Windows 8.1 升级方案。
> - 如果 ConvertibleSlateMode 无人参与设置不存在和未实现 GPIO 指示器，系统默认盖板模式。
> - ConvertibleSlateMode 无人参与设置不适用于 Windows Server 操作系统。
