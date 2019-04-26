---
title: 处理双监视器配置
description: 处理双监视器配置
ms.assetid: 224ebc3f-dace-4b41-bfc8-6fd81c8b309d
keywords:
- TMM WDK 显示、 两个监视器配置
- 监视器配置 WDK 显示两个监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 193c4aec148cdc4b5a1d92410aae083e2a0ad58d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327549"
---
# <a name="handling-two-monitor-configurations"></a>处理双监视器配置


两个监视器配置会生成 TMM 对话框。 如果两个目标是相同的图形适配器的一部分，TMM 将映射到这两个目标的目标之一当前映射的一个源。 TMM 执行映射后，将弹出 TMM 对话框。 如果目标是不同的图形适配器上，TMM 对话框将弹出无需激活第二个监视器。 在此情况下，TMM 对话框不会克隆的选项或扩展。

按以下顺序显示在其中 TMM 调用的方法的顺序[IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164)并在此情况下执行其他操作：

1.  TMM 调用**EnumDisplayDevices**函数来检索当前显示配置，其中包括适配器、 显示器和监视器。 有关详细信息**EnumDisplayDevices**，请参阅 Microsoft Windows SDK 文档。

2.  TMM 将显示针对以前记录的显示配置的配置进行比较。

3.  如果显示配置有扩展显示的信息数据与一个或两个监视器 (*EDID*) 之前，TMM 继续打开 TMM 对话框具有未遇到 TMM。

4.  为显示配置中每个适配器，TMM 会调用[ **IViewHelper::GetConnectedIDs** ](https://msdn.microsoft.com/library/windows/hardware/ff568171)方法来检索所有适配器上的源是否映射源。

5.  TMM 会调用[ **IViewHelper::GetConnectedIDs** ](https://msdn.microsoft.com/library/windows/hardware/ff568171)方法来检索所有适配器上的目标是否或未映射目标。 每个目标必须连接，但不是要求处于活动状态。

6.  每个源的图形适配器，TMM 会调用[ **IViewHelper::GetActiveTopology** ](https://msdn.microsoft.com/library/windows/hardware/ff568169)方法来检索源活动的目标。

7.  TMM 查找具有映射到目标的源的图形适配器。 此源标识符称为"CloneSource。" 如果适配器具有两个目标，TMM 创建两个项的数组 (ULONG targetArray\[2\])。 TMM 将现有的目标标识符的第一个元素和作为第二个元素的第二个目标标识符。

8.  TMM 调用[ **IViewHelper::SetActiveTopology**](https://msdn.microsoft.com/library/windows/hardware/ff568174)(adapterName，CloneSource，2，targetArray) 指示参数的方法。

9.  TMM 调用[ **IViewHelper::Commit** ](https://msdn.microsoft.com/library/windows/hardware/ff568167)方法。

如果错误结果返回的任何[IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164)方法，该计算机不会进入克隆视图和 TMM 对话框弹出与克隆视图和仅限外部的选项被禁用。

如果计算机进入克隆视图和用户可从 TMM 对话框中选择扩展的视图 (单击**确定**或**应用**)，TMM 必须先关闭克隆视图，如下所示：

1.  TMM 调用[ **IViewHelper::SetActiveTopology**](https://msdn.microsoft.com/library/windows/hardware/ff568174)(adapterName，CloneSource，1，targetArray) 指示参数的方法。

2.  TMM 调用[ **IViewHelper::Commit** ](https://msdn.microsoft.com/library/windows/hardware/ff568167)方法。

在前面**SetActiveTopology**调用时，三个参数设置为 1 且不是 2。 在此情况下， **SetActiveTopology**解释*targetArray*作为具有一个元素的数组。 **SetActiveTopology**将关闭第二个目标，并进入单一视图。 接下来，使用 TMM **ChangeDisplaySettingsEx**函数来扩展显示。 有关详细信息**ChangeDisplaySettingsEx**，请参阅 Microsoft Windows SDK 文档。

下图显示了 TMM 处理这种情况时添加一个监视器，以使两个监视器配置时发生的操作的流。

![说明添加监视器以使两个监视器配置的关系图](images/tmm-newconfig.png)

 

 





