---
title: 选项约束
description: 选项约束
keywords:
- 约束 WDK Unidrv
- 打印机选项 WDK Unidrv，约束
- 同时打印选项 WDK Unidrv
- 组合打印机选项 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 593087dbb97ba6e73c4ca46ea1ebdeacad9287c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807701"
---
# <a name="option-constraints"></a>选项约束





有时需要约束用户安装或选择与打印机功能关联的特定打印机选项的能力。 可以指定以下类型的选项约束：

-   如果已选择冲突的选项，则可以限制选项，使其无法选择。 这些约束称为 " [选择约束](selection-constraints.md)"。

-   如果已安装了冲突的可安装选项，则可以限制可安装的选项，使其无法安装。 这些约束称为 " [安装约束](installation-constraints.md)"。

-   如果已安装了冲突的可安装选项，则可以限制选项，否则无法选择该选项，如果未安装必需的可安装选项，则无法选择此选项。 这些约束在 [选择和安装之间](constraints-between-selections-and-installations.md)被称为约束。

当用户选择打印机的 "属性表" 对话框上的 **"确定"** 按钮时，驱动程序的用户界面代码将强制实施约束。 如果选择了无效的选项组合，则用户可以选择通过修改属性表页来更正冲突，或让驱动程序尝试根据 [功能冲突优先级](feature-conflict-priority.md)自动进行更正。

 

 




