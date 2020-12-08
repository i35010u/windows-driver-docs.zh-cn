---
title: 设置驱动程序功能评分
description: 设置驱动程序功能评分
keywords:
- INF 文件 WDK 显示，FeatureScore 指令
- FeatureScore 指令 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 435be4cebed21ad0f3daad35628ee9aabff1faa1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826583"
---
# <a name="setting-the-driver-feature-score"></a>设置驱动程序功能评分


在 Windows Vista 及更高版本的操作系统上安装和运行的所有驱动程序都需要 **FeatureScore** 指令。

**注意**   仅适用于 Windows 7 及更高版本。
系统提供的显示类安装程序基于是否存在 **FeatureScore** 指令以及 **FeatureScore** 指令设置的值来确定是否安装显示驱动程序。 如果尝试安装未设置功能分数的显示驱动程序，将收到一条错误消息。

 

**注意**   徽标测试要求是在 Windows XP 及更早版本的操作系统和 Windows Server 2003 及更早版本的操作系统上安装和运行的驱动程序未设置 **FeatureScore** 指令。

 

您必须使用 **FeatureScore** 指令将特征分数设置为以下值，具体取决于驱动程序所写入的显示驱动程序模型以及如何分发该驱动程序。

-   用于写入 Windows 显示驱动程序模型 (WDDM) 的内置驱动程序的 **F8**

-   **F6** ，用于写入 WDDM 的供应商提供的驱动程序

-   写入到 [Windows 2000 显示驱动程序模型](windows-2000-display-driver-model-design-guide.md)中供应商提供的驱动程序的 **FC**

下面的示例演示如何添加 **FeatureScore** 指令：

```inf
[R200_RV200]
FeatureScore=F6
CopyFiles=R200.Miniport, R200.Display
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_RV200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings

[R200_R200]
FeatureScore=F6
CopyFiles=R200.Miniport, R200.Display
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_R200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings

[R200_RV250]
FeatureScore=F6
CopyFiles=R200.Miniport, R200.Display
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_RV250_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings
```

 
