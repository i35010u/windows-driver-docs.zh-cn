---
title: 处理双监视器配置
description: 处理双监视器配置
ms.assetid: 224ebc3f-dace-4b41-bfc8-6fd81c8b309d
keywords:
- TMM WDK 显示，两个监视器配置
- 监视器配置 WDK 显示，两监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96396d991c6ffaee7e84d5fb00cefe0b41275bf4
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065822"
---
# <a name="handling-two-monitor-configurations"></a>处理双监视器配置


双监视器配置将生成 "TMM" 对话框。 如果两个目标属于同一图形适配器，则 TMM 会将当前映射到其中一个目标的源映射到这两个目标。 TMM 执行映射后，将弹出 TMM 对话框。 如果目标在不同的图形适配器上，则将弹出 TMM 对话框而不激活第二个监视器。 在这种情况下，TMM 对话框不会有用于克隆或扩展的选项。

以下顺序显示了 TMM 调用 [IViewHelper](/windows-hardware/drivers/ddi/index) 方法的顺序，以及在这种情况下执行其他操作：

1.  TMM 调用 **EnumDisplayDevices** 函数来检索当前显示配置，其中包括适配器、显示和监视器。 有关 **EnumDisplayDevices**的详细信息，请参阅 Microsoft Windows SDK 文档。

2.  TMM 将显示配置与以前记录的显示配置进行比较。

3.  如果显示配置具有一个或两个监视器，其中包含扩展的显示信息数据 (*EDID*) 之前尚未遇到 TMM，则 TMM 将继续显示 TMM 对话框。

4.  对于显示配置中的每个适配器，TMM 会调用 [**IViewHelper：： GetConnectedIDs**](/previous-versions/windows/hardware/drivers/ff568171(v=vs.85)) 方法，以便在适配器上检索所有源是否已映射。

5.  TMM 调用 [**IViewHelper：： GetConnectedIDs**](/previous-versions/windows/hardware/drivers/ff568171(v=vs.85)) 方法来检索适配器上的所有目标，无论目标是否已映射。 每个目标都必须连接，但不需要处于活动状态。

6.  对于图形适配器中的每个源，TMM 会调用 [**IViewHelper：： GetActiveTopology**](/previous-versions/windows/hardware/drivers/ff568169(v=vs.85)) 方法来检索源的活动目标。

7.  TMM 查找具有映射到目标的源的图形适配器。 此源标识符名为 "CloneSource"。 如果适配器有两个目标，则 TMM 将创建一个包含两个条目的数组， (ULONG targetArray \[ 2 \]) 。 TMM 将现有目标标识符放置为第一个元素，将第二个目标标识符放置为第二个元素。

8.  TMM 调用 [**IViewHelper：： SetActiveTopology**](/previous-versions/windows/hardware/drivers/ff568174(v=vs.85)) (AdapterName，CloneSource，2，targetArray) 方法替换为指定的参数。

9.  TMM 调用 [**IViewHelper：： Commit**](/previous-versions/windows/hardware/drivers/ff568167(v=vs.85)) 方法。

如果在任何 [IViewHelper](/windows-hardware/drivers/ddi/index) 方法中返回错误结果，则计算机不会输入克隆视图，并且会弹出 TMM 对话框，其中禁用了克隆视图和仅限外部选项。

如果计算机输入克隆视图，并且用户从 "TMM" 对话框中选择 "扩展视图" (然后单击 **"确定" 或 "** **应用**) "，则 TMM 必须关闭克隆视图，如下所示：

1.  TMM 调用 [**IViewHelper：： SetActiveTopology**](/previous-versions/windows/hardware/drivers/ff568174(v=vs.85)) (AdapterName，CloneSource，1，targetArray) 方法和指定的参数。

2.  TMM 调用 [**IViewHelper：： Commit**](/previous-versions/windows/hardware/drivers/ff568167(v=vs.85)) 方法。

在前面的 **SetActiveTopology** 调用中，参数三设置为1，而不是2。 在这种情况下， **SetActiveTopology** 将 *targetArray* 解释为具有一个元素的数组。 **SetActiveTopology** 关闭第二个目标并进入单一视图。 接下来，TMM 使用 **ChangeDisplaySettingsEx** 函数来扩展显示。 有关 **ChangeDisplaySettingsEx**的详细信息，请参阅 Microsoft Windows SDK 文档。

下图显示了在添加监视器以进行双监视器配置时，TMM 处理此情况时所发生的操作流。

![说明如何添加监视器以进行双监视器配置的关系图](images/tmm-newconfig.png)

 

