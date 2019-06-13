---
ms.assetid: A1DE1065-9D8F-405F-9807-5F0D3BE6F0AC
title: 驱动程序签名属性
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa3d8b39490757d3ec01d31670cca8a322f4894d
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63391516"
---
# <a name="driver-signing-properties"></a>驱动程序签名属性

在“解决方案资源管理器”中选择项目时，“驱动程序签名”  节点下的“属性”  对话框将显示属性的两个部分：

## <a name="span-idundergeneralspanspan-idundergeneralspanspan-idundergeneralspanunder-general"></a><span id="Under_General_"></span><span id="under_general_"></span><span id="UNDER_GENERAL_"></span>在“常规”下：


**签名模式**

-   **测试签名** - Microsoft Visual Studio 应使用**测试证书**中指定的测试证书签署驱动程序（默认）。 如果未在**测试证书**中指定证书，Visual Studio 会为驱动程序创建一个证书。 **注意**：Windows 需要签署所有 64 位驱动程序。
-   **生产签名** - Visual Studio 应使用**生产证书**中指定的生产证书签署驱动程序。
-   **关闭** - Visual Studio 不应使用任何证书签署驱动程序。

**测试证书**

-   *空白* - 未选择测试证书（默认）。
-   **&lt;编辑…&gt;** - 选择将“签名模式”  设置为“测试签名”  时要使用的证书。

**生产证书**

-   *空白* - 未选择生产证书（默认）。
-   **&lt;编辑…&gt;** - 选择将“签名模式”  设置为“生产签名”  时要使用的证书。

**TimeStampServer**

-   **Verisign** - 使用 Verisign 为驱动程序添加时间戳（默认）。
-   **GlobalSign** - 使用 Globalsign 为驱动程序添加时间戳。
-   **无** - 不为驱动程序添加时间戳。

**禁用警告**

-   **否** - 签署驱动程序时显示警告（默认）。
-   **是** - 签署驱动程序时不显示警告。

**启用诊断详细级别**

-   **否** - 签署驱动程序时不显示诊断详细级别（默认）。
-   **是** - 签署驱动程序时显示诊断详细级别。

**文件摘要算法**

-   *空白* - 未选择文件摘要算法（默认）。
-   **&lt;编辑…&gt;** - 选择在签署驱动程序时要使用的文件摘要算法。

## <a name="span-idundercommandlinespanspan-idundercommandlinespanspan-idundercommandlinespanunder-command-line"></a><span id="Under_Command_Line_"></span><span id="under_command_line_"></span><span id="UNDER_COMMAND_LINE_"></span>在命令行下：


**其他选项**

-   签署驱动程序时要指定的其他选项。

 

 





