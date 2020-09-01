---
title: 网络 INF 文件中的 Models 节
description: 网络 INF 文件中的 Models 节
ms.assetid: 0340a875-ae5a-49c8-9498-1f8aba97e029
keywords:
- INF 文件 WDK 网络，模型部分
- 网络 INF 文件 WDK，型号部分
- 型号部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80d7a50d2fc6e77b285c880ff9ec1a9937e5eb9b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212373"
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

*提供程序名称*标识 INF 文件的提供程序。 *制造商名称*标识软件组件的制造商。 *产品名称*标识软件组件。

 

