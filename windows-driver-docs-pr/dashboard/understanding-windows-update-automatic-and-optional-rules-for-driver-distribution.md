---
title: 使用 Windows 更新安装驱动程序
description: 本主题介绍如何控制 Windows 更新何时分发驱动程序。
ms.date: 05/28/2019
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 0d441fa727b8ea5295eabf0ac553010e594bf80f
ms.sourcegitcommit: c94be6fc464edc94035060a4723efa06ab0f5af9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92153471"
---
# <a name="understanding-windows-update-automatic-and-optional-rules-for-driver-distribution"></a>了解适用于驱动程序分发的 Windows 更新自动和可选规则

本文介绍如何控制 Windows 更新何时分发驱动程序。

[向 Windows 更新提交驱动程序](publish-a-driver-to-windows-update.md)时，“驱动程序交付选项”部分会显示两个单选按钮：“自动”和“手动” 

在“自动”选项下有两个复选框：“在 Windows 更新期间自动交付”和“自动交付到所有适用系统” 。 “自动”是所有新发货标签的默认设置。

![自动驱动程序推广复选框](images/driver-delivery-options.png)

选中第一个复选框时，该驱动程序将归类为“动态更新”（适用于“升级”场景的术语）。 升级操作系统时，Windows 会自动预加载此类别中的驱动程序。

选中第二个复选框时，将在驱动程序发布后在所有适用的系统上自动下载并安装该驱动程序。 所有“自动”驱动程序必须首先由 Microsoft 通过[驱动程序外部测试](driver-flighting.md)进行评估。

有关“手动”选项的详细信息，请参阅[将驱动程序发布到 Windows 更新](publish-a-driver-to-windows-update.md)。

## <a name="automatic-updates"></a>自动更新

在计划的更新期间或在用户选择“更新与安全性”设置菜单中的“检查更新”时，Windows 更新将仅分发适用于系统设备的排名最高的自动驱动程序。

## <a name="optionalmanual-updates"></a>可选/手动更新

在 Windows 10 版本 1909 及更低版本中，Windows 更新会在以下情况中自动分发“可选/手动”驱动程序：
* 设备在驱动程序存储中没有任何适用的驱动程序（“未找到驱动程序”），并且没有适用的“自动”驱动程序
* 或者，唯一本地可用的驱动程序是通用的，这意味着该驱动程序是系统提供的，只提供基本的设备功能，并且没有适用的“自动”驱动程序

## <a name="device-plug-in-plug-and-play"></a>设备插件（“即插即用”）

设备连接到 Windows 系统时，[即插即用 (PnP)](../kernel/introduction-to-plug-and-play.md) 将查找计算机中提供的兼容驱动程序。 如果找到，Windows 会将其安装在设备上。 否则，Windows 将搜索 Windows 更新以获取兼容的驱动程序，首先会匹配 Windows 更新上排名最高的“自动”驱动程序。

在 Windows 10 版本 1909 及更低版本中，如果没有可用于该设备的“自动”驱动程序，Windows 将继续查找排名最高的“可选/手动”驱动程序 。

从 Windows 10 版本 2004 开始，当“自动”驱动程序不可用时，Windows 不会搜索“可选/手动”驱动程序 。 若要访问“可选/手动”驱动程序，请转到：“设置”>“更新和安全”>“Windows 更新”>“查看可选更新”>“驱动程序更新”。

## <a name="device-manager"></a>设备管理器

在 Windows 10 版本 1909 及更低版本中，当用户在设备管理器中搜索更新的驱动程序时，Windows 将尝试从 Windows 更新安装排名最高的驱动程序，无论它是被归类为“自动”还是“可选/手动” 。

从 Windows 10 版本 2004 开始，当用户在设备管理器中搜索更新的驱动程序时，Windows 仅会搜索计算机上的驱动程序。 若要联机搜索，请使用“Windows 更新设置”页面。

## <a name="summary"></a>摘要

下表汇总了上述信息。

第一列指示“驱动程序交付选项”部分中的选择状态。 第一个复选框（“在 Windows 更新期间自动交付”）由“动态更新”指示，第二个复选框（“自动交付到所有适用系统”）由常规的“自动”更新指示  。 “手动”指示“可选/手动”驱动程序，Windows 更新简写为 WU 。

|驱动程序交付选项|操作系统升级|连接新设备|设备管理器|Windows 更新每日扫描或“检查更新”按钮|Windows 更新“可选”页|
|-|-|-|-|-|-|
|自动（默认值）|是|仅当本地驱动程序是通用的或缺失时|仅在 Windows 10 版本 1909 及更低版本中|是|否|
|仅限常规的自动更新|否|仅当本地驱动程序是通用的或缺失时|仅在 Windows 10 版本 1909 及更低版本中|是|否|
|仅“动态更新”|是|仅当本地驱动程序是通用的或缺失，并且 WU 没有适用的“自动”驱动程序时|仅在 Windows 10 版本 1909 及更低版本中|仅当本地驱动程序是通用的或缺失，并且 WU 没有适用的“自动”驱动程序时|否|
|在 Windows 10 版本 1909 及更低版本中为“手动”|否|仅当本地驱动程序是通用的或缺失，并且 WU 没有适用的“自动”驱动程序时|是|仅当本地驱动程序是通用的或缺失，并且 WU 没有适用的“自动”驱动程序时|否|
|从 Windows 10 版本 2004 开始为“手动”|否|否|否|否|否|

