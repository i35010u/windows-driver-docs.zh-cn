---
title: 使用 Windows 更新安装驱动程序
description: 本主题介绍如何控制 Windows 更新何时分发驱动程序。
ms.date: 11/02/2020
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 4ef0d34f59dc13726f42244e684a3fdd5ebaec5d
ms.sourcegitcommit: 255ecc7bee00df8bee1f097f6ba3e4179aba0251
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328144"
---
# <a name="understanding-windows-update-rules-for-driver-distribution"></a>了解适用于驱动程序分发的 Windows 更新规则

本文介绍如何控制 Windows 更新何时分发驱动程序。

[向 Windows 更新提交驱动程序](publish-a-driver-to-windows-update.md)时，“驱动程序交付选项”部分会显示两个单选按钮：“自动”和“手动” 

在“自动”选项下有两个复选框：“在 Windows 升级期间自动交付”和“自动交付到所有适用系统” 。 “自动”是所有新发货标签的默认设置。

![自动驱动程序推广复选框](images/driver-delivery-options.png)

选中第一个复选框时，该驱动程序将归类为“动态更新”（适用于“升级”场景的术语）。 升级操作系统时，Windows 会自动预加载此类别中的驱动程序。

选中第二个复选框时，将在驱动程序发布后在所有适用的系统上自动下载并安装该驱动程序。 所有“自动”驱动程序必须首先由 Microsoft 通过[驱动程序外部测试](driver-flighting.md)进行评估。

有关“手动”选项的详细信息，请参阅[将驱动程序发布到 Windows 更新](publish-a-driver-to-windows-update.md)。

## <a name="user-plugs-in-a-device"></a>用户插入设备

当设备连接到 Windows 系统时：

* [即插即用 (PnP)](../kernel/introduction-to-plug-and-play.md) 将查找计算机中提供的兼容驱动程序。 如果找到，Windows 会将其安装在设备上。 然后，在 Windows 更新的下次每日扫描时，Windows 会搜索更新版本的驱动程序。 从插入设备时算起，这最多需要 24 小时的时间。

* 如果计算机上没有兼容的驱动程序，则 Windows 将搜索 Windows 更新来排名最高的“自动”驱动程序。

搜索 Windows 更新时：

* 在 Windows 10 版本 1909 及更低版本中，如果没有可用于该设备的“自动”驱动程序，Windows 将继续查找排名最高的“手动”驱动程序 。

* 从 Windows 10 版本 2004 开始，当“自动”驱动程序不可用时，Windows 不会搜索“手动”驱动程序 。 若要了解如何访问“手动”驱动程序，请参阅本页的 [Windows 更新](#windows-update)部分。

## <a name="device-manager"></a>设备管理器

在设备管理器中，当用户选择“更新驱动程序”时：

* 在 Windows 10 版本 1909 及更低版本中，Windows 将尝试从 Windows 更新安装排名最高的驱动程序，无论它是被归类为“自动”还是“手动”都是如此 。
* 从 Windows 10 版本 2004 开始，Windows 仅搜索本地计算机。

如果找不到驱动程序，设备管理器会显示一个标记为“在 Windows 更新上搜索已更新的驱动程序”按钮，这会打开“设置”应用转到“Windows 更新”页面。 若要查找此按钮，请右键单击一个设备，然后选择“属性”。 在“驱动程序”选项卡上，选择“更新驱动程序”，然后选择“自动搜索驱动程序”  。

* 从 Windows 10 版本 2004 开始，单击“在 Windows 更新上搜索已更新的驱动程序”，然后选择“查看可选更新”->“驱动程序更新”，下载“手动”驱动程序  。
* 在更低版本的 Windows 中，设备管理器会自行下载“手动”驱动程序。

## <a name="windows-update"></a>Windows 更新

在 Windows 更新扫描期间（按照计划或由用户发起）：

* 在 Windows 10 版本 1909 及更低版本中，Windows 更新会在遇到下述任一情况时自动分发“手动”驱动程序：

    * 设备在驱动程序存储中没有任何适用的驱动程序（引发“未找到驱动程序”错误），并且没有适用的“自动”驱动程序
    * 设备在驱动程序存储中只有通用驱动程序，该程序只提供基本的设备功能，而且不存在适用的“自动”驱动程序

* 从 Windows 10 版本 2004 开始，Windows 更新仅为系统的设备分发“自动”驱动程序。 当“手动”驱动程序可用于计算机上的设备时，“设置”应用中的“Windows 更新”页面会显示”查看可选更新” 。

## <a name="summary"></a>摘要

下表总结了上述信息。 Windows 更新缩写为 WU。

|驱动程序传递选项|操作系统升级|连接新设备|设备管理器|WU 扫描|WU 可选更新页面|
|-|-|-|-|-|-|
|自动（两个复选框）|是|仅当本地驱动程序是通用的或缺失时|仅在 Windows 10 版本 1909 及更低版本中|是|否|
|自动（针对所有适用系统）|否|仅当本地驱动程序是通用的或缺失时|仅在 Windows 10 版本 1909 及更低版本中|是|否|
|自动（在 Windows 升级期间）|是|仅当本地驱动程序是通用的或缺失时|仅在 Windows 10 版本 1909 及更低版本中|仅当本地驱动程序是通用的或缺失时|否|
|在 Windows 10 版本 1909 及更低版本中为“手动”|否|仅当本地驱动程序是通用的或缺失，并且 WU 没有适用的“自动”驱动程序时|是|仅当本地驱动程序是通用的或缺失，并且 WU 没有适用的“自动”驱动程序时|空值|
|在 Windows 10 版本 2004 及更高版本中为“手动”|否|否|否|否|是|

