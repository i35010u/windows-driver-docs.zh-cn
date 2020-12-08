---
title: 构建 PSHED 插件
description: 构建 PSHED 插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee7bea814323c469cba66985bb4c0f0f81feac1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795771"
---
# <a name="building-a-pshed-plug-in"></a>构建 PSHED 插件


PSHED 插件是使用 WDK 构建的，与任何其他 Windows 驱动模型 (WDM) 设备驱动程序一样，除了除了链接到内核和硬件抽象层 (HAL) 之外，PSHED 插件还必须显式链接到 *PSHED*。

**注意**  从 Windows 7 开始，已从 WHEA 的早期版本重命名了各种 Windows 硬件错误体系结构 (的) 数据类型。 有关这些更改的详细信息，请参阅 [重命名的 WHEA 数据类型](renamed-whea-data-types.md)。 如果你计划使用 Windows 7 或更高版本的 WDK 构建现有的 PSHED 插件，你仍可以使用以前的 WHEA 数据类型名称。 为此，请将以下信息添加到用于生成插件的 *源文件* 中： `C_DEFINES = $(C_DEFINES) /DWHEA_DOWNLEVEL_TYPE_NAMES`

 

 

 




