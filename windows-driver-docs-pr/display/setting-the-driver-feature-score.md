---
title: 设置驱动程序功能评分
description: 设置驱动程序功能评分
ms.assetid: 833e8f29-b90a-4754-9c0a-d8356a731ae4
keywords:
- INF 文件 WDK 显示、 FeatureScore 指令
- FeatureScore 指令 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b6ab89db8104ef636baac8990b0f3e79b930aa7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568008"
---
# <a name="setting-the-driver-feature-score"></a>设置驱动程序功能评分


**FeatureScore**指令是所必需的所有驱动程序的 Windows Vista 和更高版本操作系统上安装和运行。

**请注意**  仅适用于 Windows 7 和更高版本。
系统提供显示类安装程序将确定是否安装显示器驱动程序基于是否存在**FeatureScore**指令和值的**FeatureScore**指令集。 如果你尝试安装不具有设置的特征评分的显示器驱动程序，你将收到一条错误消息。

 

**请注意**  徽标测试要求是 Windows XP 和早期版本的操作系统和 Windows Server 2003 和早期版本的操作系统安装和运行的驱动程序未设置**FeatureScore**指令。

 

必须使用**FeatureScore**指令设置为以下值，具体取决于驱动程序写入到显示器驱动程序模型和如何分发驱动程序的特征评分。

-   **F8**写入到 Windows 显示器驱动程序模型 (WDDM) 的现成驱动程序

-   **F6**写入 WDDM 供应商提供驱动程序

-   **FC**供应商提供的驱动程序写入到[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)

以下示例演示如何添加**FeatureScore**指令：

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

 
