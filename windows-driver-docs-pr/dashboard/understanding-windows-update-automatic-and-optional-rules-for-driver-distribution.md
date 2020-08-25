---
title: 使用 Windows 更新安装驱动程序
description: 本主题介绍如何控制 Windows 更新何时分发驱动程序。
ms.date: 05/28/2019
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: a52e9e4e476b1f4dc099d4c60f8b2813a410c5ea
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252995"
---
# <a name="understanding-windows-update-automatic-and-optional-rules-for-driver-distribution"></a>了解适用于驱动程序分发的 Windows 更新自动和可选规则

> [!NOTE]
> 下面列出的行为适用于 Windows 10 版本 1709 及更高版本。

本文介绍如何控制 Windows 更新何时分发驱动程序。

[向 Windows 更新提交驱动程序](publish-a-driver-to-windows-update.md)时，“驱动程序推广”  部分会显示两个复选框：“在 Windows 升级期间自动传递并安装此驱动程序”  和“在所有适用系统上自动传递并安装此驱动程序”  。

![自动驱动程序推广复选框](images/automatic-driver-promotion-options.png)

如果选中第一个复选框，则该驱动程序将归类为“动态更新”  （适用于“升级”  场景的术语）。 之后，Windows 会在升级操作系统时自动预加载该驱动程序。

如果选中第二个复选框，则该驱动程序将归类为“自动”  （以前称为“关键更新”  ）；如果未选中，则该驱动程序将归类为“可选”  。  若要作为“自动”  向 Windows 更新发布，驱动程序必须先由 Microsoft 通过[驱动程序外部测试](driver-flighting.md)进行评估。

## <a name="automatic-updates"></a>自动更新

在计划的更新期间或在用户选择“更新与安全性”设置菜单中的“检查更新”时，Windows 更新将仅分发适用于系统设备的排名最高的自动驱动程序。 **自动驱动程序**是提供基本设备功能的系统驱动程序或自带的驱动程序。 如果存在以下情况，Windows 更新只会分发**可选的**驱动程序：

* 设备在驱动程序存储中没有任何适用的驱动程序（“未找到驱动程序”）
* 或者，只有本地可用的驱动程序是通用的，即，只有本地可用的驱动程序是系统提供的驱动程序，该驱动程序只提供基本设备功能。 

## <a name="device-plug-in-plug-and-play"></a>设备插件（“即插即用”）

设备连接到 Windows 系统时，[即插即用 (PnP)](../kernel/introduction-to-plug-and-play.md) 将查找已在系统中本地提供的兼容驱动程序。 如果找到，Windows 会将其安装在设备上。 否则，Windows 将在 Windows 更新上查找兼容的驱动程序，首先匹配 Windows 更新上排名最高的**自动**驱动程序。 如果没有可用于该设备的**自动**驱动程序，Windows 将继续查找排名最高的**可选**驱动程序。

当驱动程序存储中没有插入式设备适用的驱动程序（“未找到驱动程序”），或唯一可用的本地驱动程序是“通用”  驱动程序时，则该逻辑同样适用。

## <a name="device-manager"></a>设备管理器

当用户在设备管理器中搜索更新的驱动程序时，Windows 将尝试从 Windows 更新安装排名最高的驱动程序，无论它是被归类为**自动**还是**可选**.

## <a name="summary"></a>摘要

下表汇总了上述信息。

第一列指示“驱动程序推广”  部分的两个复选框哪一个被选中。
第一个复选框（**在 Windows 升级期间自动传递并安装此驱动程序**）由“动态更新”指示，第二个复选框（**在所有适用的系统上自动传递并安装此驱动程序**）由“自动”指示。 Windows 更新缩写为 WU。

|选中的驱动程序推广框|Windows 更新（已计划或通过“更新与安全性”|操作系统升级|连接新设备|设备管理器|
|-|-|-|-|-|
|仅“自动”|是|否|仅当本地驱动程序是通用的/缺失时。|是|
|仅“动态更新”|仅当本地驱动程序是通用的/缺失，并且 WU 没有适用的**自动**驱动程序时|是|仅当本地驱动程序是通用的/缺失，并且 WU 没有适用的**自动**驱动程序时|是|
|双向|是|是|仅当本地驱动程序是通用的/缺失时。|是|
|两者均未选中|仅当本地驱动程序是通用的/缺失，并且 WU 没有适用的**自动**驱动程序时|否|仅当本地驱动程序是通用的/缺失，并且 WU 没有适用的**自动**驱动程序时|是|

<!--use word generic? or just condense descriptive text?-->
