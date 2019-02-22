---
title: Static Driver Verifier 错误消息
description: Static Driver Verifier 错误消息
ms.assetid: 16fae27c-2495-4b54-9df8-b70ad20d30ab
keywords:
- 静态驱动程序验证程序 WDK 错误
- StaticDV WDK 错误
- SDV WDK 错误
- 消息 WDK Static Driver Verifier
- 错误 WDK Static Driver Verifier
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: fdbc8ed12a58a59cbd347c88b1c44b3f4dde888c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524661"
---
# <a name="static-driver-verifier-error-messages"></a>Static Driver Verifier 错误消息


本部分介绍的一些更频繁地看到 SDV 错误含义消息并建议解决问题的方法。

启动 Visual Studio 中的 SDV，可能会看到以下错误：

* **SDV 仅可在非调试配置上运行**:如消息指出，必须在非调试配置上运行 SDV。  请确保你的项目设置为发布配置或如果没有，则创建一个然后重新启动 SDV。
* **时出错，正在加载可用规则**:SDV 是找不到您的驱动程序的规则的模型或无法确定正确的驱动程序模型 （更有可能是如果您的驱动程序不是 WDM、 KMDF、 NDIS 或 Storport 驱动程序）。  如果正确安装在 WDK，您可能能够通过直接从命令行运行 SDV 来解决此错误 (请参阅[Static Driver Verifier 命令 (MSBuild)](-static-driver-verifier-commands--msbuild-.md))。
* **SDV 无法清除的驱动程序目录**:在某些情况下，权限错误可能会阻止 SDV 在单击"清除"按钮时正确清理旧结果从驱动程序目录。  如果之前运行 sdv 文件当前正在使用，也将出现此错误。  请确保执行任何操作使用您的驱动程序目录中的 SDV 文件，然后删除任何"sdv"和"sdv.temp"文件夹和"staticdv.job"的任何文件。

如果 SDV 失败尝试分析时，它将打印到标准输出中失败的阶段。  从 Visual Studio 图形用户界面运行 SDV 时，可以切换到"警报"选项卡中看到以下输出。

SDV 中可能会失败的阶段包括：
* **NormalBuild**:SDV 无法生成使用标准的 MSBuild 命令的驱动程序。  如果有专门的生成逻辑、 在项目文件中，依赖于解决方案元素或具有外部生成组件，这可能会出现。  如果你的项目依赖于 $ （solutiondir） 属性，您可以将该变量提供直接通过重新从命令行运行 SDV，并将其追加到命令行通过添加 **/p:SolutionDir =\[解决方案 dir\]** 到 MSBuild 命令的末尾。  请参阅[Static Driver Verifier 命令 (MSBuild)](-static-driver-verifier-commands--msbuild-.md)。
* **InterceptedBuild**:SDV 无法生成以进行分析驱动程序。  
* **扫描**:SDV 找不到驱动程序的入口点。  此处的错误可能表示不找到的任何入口点，并应更新你的函数 roletypes 或 sdv map.h。  请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)并[批准 Sdv map.h 文件](approving-the-sdv-map-h-file.md)有关详细信息。
* **FinalCompile**:SDV 无法编译您的驱动程序与规则和 OS 模型。
* **CheckRule**:SDV 无法正确验证的规则。

您可以通过启用诊断的 SDV 了解有关错误的更多详细信息。  请参阅[静态驱动程序验证工具诊断](static-driver-verifier-diagnostics.md)有关详细信息。
