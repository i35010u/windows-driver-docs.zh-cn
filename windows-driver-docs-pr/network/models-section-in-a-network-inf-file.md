---
title: 网络 INF 文件中的 Models 节
description: 网络 INF 文件中的 Models 节
keywords:
- INF 文件 WDK 网络，模型部分
- 网络 INF 文件 WDK，型号部分
- 型号部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56c790b3f7b3b31b5f026bae348126496eb1c8ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836771"
---
# <a name="models-section-in-a-network-inf-file"></a>网络 INF 文件中的 Models 节





网络 INF 文件中的 " **模型** " 部分基于 "通用 [**INF 模型" 部分**](../install/inf-models-section.md)。

INF 文件中的 " **模型** " 部分对于 inf 文件所安装的每种类型的组件，都包含以下格式的条目：

\[*设备-描述* = *install-section.name*， *hw-id* \[ ，*兼容-id*.。。\]

有关此项的详细说明，请参阅 [创建 INF 文件](../install/overview-of-inf-files.md)。

*Hw id* (也称为网络适配器的设备、硬件或组件 id) 必须与适配器提供给 PnP 管理器的硬件 id 匹配。

网络软件组件的 *硬件 id* 应该包含提供程序名称、下划线以及制造商名称或产品名称，例如：

-   MS \_ DLC

-   MS \_ IBMDLC

*提供程序名称* 标识 INF 文件的提供程序。 *制造商名称* 标识软件组件的制造商。 *产品名称* 标识软件组件。

 

