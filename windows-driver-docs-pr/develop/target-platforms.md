---
ms.assetid: EB2264A4-BAE8-446B-B9A5-19893936DDCA
title: 驱动程序参考页的目标平台
description: 在 Microsoft 驱动程序参考页底部的“要求”块中，将看到一个称为“目标平台”的条目。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc571594ab09e403673c388d3e56669b4849c46b
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769655"
---
# <a name="target-platform-on-driver-reference-pages"></a>驱动程序参考页上的“目标平台”

在 Microsoft 驱动程序参考页底部的“要求”块中，将看到一个称为“目标平台”的条目。 该行列出了页面将应用到的 Windows 版本。

以下是此类条目的示例：

![目标平台在“要求”块中设置为“通用”](images/TargetPlatform.png)

在“目标平台”中指定的值映射到可以在 Visual Studio 中使用的值（在“配置属性”->“驱动程序设置”->“常规”下的“目标平台”属性中）。  Windows 驱动程序可以使用任何将“通用”指定为目标平台的 DDI。

以下是你可能看到的**目标平台**的值以及它们的含义：

|术语|说明|
|--- |--- |
|通用|Windows 驱动程序中的驱动程序二进制文件可以调用此设备驱动程序接口 (DDI)。 有关详细信息，请参阅 [Windows 驱动程序入门](getting-started-with-windows-drivers.md)。|
|台式机|Windows 10 桌面版或 Windows Server 2016 的驱动程序二进制文件可以调用此 DDI。|

Windows 驱动程序在以下基于通用 Windows 平台 (UWP) 的 Windows 10 版本上运行：

*   Windows 10 桌面版（家庭版、专业版和企业版）
*   处于 S 模式的 Windows 10
*   Windows 10 IoT 核心版
*   Windows Server 2016


