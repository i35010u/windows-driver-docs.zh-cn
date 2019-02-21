---
title: 选项约束
description: 选项约束
ms.assetid: dc399715-c238-4a6e-8ce0-3204aa0cca68
keywords:
- 约束 WDK Unidrv
- 打印机选项 WDK Unidrv，约束
- 同时打印机选项 WDK Unidrv
- 组合打印机选项 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50f8d391fc65573e6f37e76844e1f49852af27d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525261"
---
# <a name="option-constraints"></a>选项约束





此外，有时需要限制用户可安装或选择特定打印机选项与打印机功能相关联的功能。 可以指定以下选项约束的类型：

-   因此，如果已选中冲突的选项，则您无法选中它，可以约束选项。 这些约束称为[选择约束](selection-constraints.md)。

-   因此，如果已安装冲突的可安装选项，则不能安装此，可以约束的可安装选项。 这些约束称为[安装约束](installation-constraints.md)。

-   可以限制选项，以使其不能选中如果冲突的可安装选项已安装或未安装，以便它不能选择如果所需的可安装选项。 这些约束称为[之间的选择和安装的约束](constraints-between-selections-and-installations.md)。

驱动程序的用户界面代码强制执行约束，当用户选择**确定**打印机的属性表对话框上的按钮。 如果选择了无效的选项组合，用户是选择或者通过修改属性表页更正冲突，或让驱动程序会尝试自动进行的更正基于[功能冲突优先级](feature-conflict-priority.md)。

 

 




