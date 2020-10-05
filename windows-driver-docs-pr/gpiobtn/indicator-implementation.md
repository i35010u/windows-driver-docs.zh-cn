---
title: 指示器实现
description: 本主题介绍指标实现。
ms.assetid: 60BCE8C7-416E-4D5B-9B32-9B398CEA6A8A
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26d2b4453de14da59d7ae3b4e79e0b6058c89ac7
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734087"
---
# <a name="indicator-implementation"></a>指示器实现

本主题介绍指标实现。

由于传感器布局和相关逻辑是特定于系统的，因此，在系统执行任何相关的电源转换（如下所示）时，请务必更新模式：

- 已连接待机
- 进入睡眠或休眠状态
- 启动后

这会强制使用正确的状态，并确保刷新用户界面层。

## <a name="laptopslate-mode---implementation-for-convertibles"></a>笔记本电脑/石板模式-改装的实现

*图1可转换的实现选项* 显示在转换的系统上实现 GPIO 指示器的选项。

![可转换的实现选项](images/implementationconvertibles.jpg)

图1可转换实现选项

## <a name="laptopslate-mode---implementation-for-laptops"></a>笔记本电脑/石板模式-便携式计算机的实现

*图2笔记本电脑实现选项* 显示用于在便携式系统上实施 GPIO 指示器的选项。

![笔记本电脑实现选项](images/implementationlaptops.jpg)

图2笔记本电脑实现选项

使用 ConvertibleSlateMode [无人参与 Windows 安装程序](/previous-versions/windows/it-pro/windows-8.1-and-8/ff699026(v=win.10)) 设置，oem 可以在不实现注入机制的情况下将 clamshells 以静态方式标记为作为图像自定义的便携式计算机模式。

此功能面向具有永久连接键盘 (的触摸屏系统，用户可以随时使用) 。 此处提供的示例是没有可用的 GPIO 指示器/注入的触摸屏 clamshell。

此设置必须作为专用配置阶段的一部分应用，并且可以应用于所有 Windows 客户端操作系统。 有关详细信息，请参阅 [确定无人参与设置传递](https://sharepoint/sites/cba/Wiki Pages/Identifying Unattend Setting Passes.aspx) 。

有关代码示例，请参阅。

> [!NOTE]
>
> - 加载 GPIO 按钮驱动程序会替代通过无人参与设置引入的值。
> - 注入机制可与 Windows 8.1 系统一起使用。
> - ConvertibleSlateMode 无人参与设置不影响 Windows 8 Windows 8.1 升级方案。
> - 如果 ConvertibleSlateMode 无人参与设置不存在并且未实现 GPIO 指示器，则系统默认为石板模式。
> - ConvertibleSlateMode 无人参与设置不适用于 Windows Server 操作系统。