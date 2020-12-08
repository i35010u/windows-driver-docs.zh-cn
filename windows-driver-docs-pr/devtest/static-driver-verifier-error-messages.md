---
title: 静态驱动程序验证程序错误消息
description: 静态驱动程序验证程序错误消息
keywords:
- 静态驱动程序验证程序 WDK，错误
- StaticDV WDK，错误
- SDV WDK，错误
- 消息 WDK 静态驱动程序验证程序
- 错误 WDK 静态驱动程序验证程序
ms.date: 04/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d3d05e667dfe70cdb210980210e6c85f6111fe9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791909"
---
# <a name="static-driver-verifier-error-messages"></a>静态驱动程序验证程序错误消息


本部分说明一些更常见的 SDV 错误消息的含义，并提供解决这些错误消息的建议方法。

从 Visual Studio 启动 SDV 时，你可能会看到以下错误：

* **SDV 仅对非调试配置进行操作**：如消息所示，SDV 必须在非调试配置上运行。  请确保将项目设置为 "发布" 配置，如果该配置不可用，请创建一个，并重新启动 SDV。
* **加载可用规则时出错**： SDV 找不到驱动程序模型的规则，或者无法正确确定驱动程序模型 (如果驱动程序不是 WDM、KMDF、NDIS 或 Storport 驱动程序) ，则更有可能。  如果已正确安装了 WDK，则可以通过直接从命令行运行 SDV 来解决此错误， (参阅 [静态驱动程序验证程序命令 (MSBuild) ](-static-driver-verifier-commands--msbuild-.md)) 。
* **SDV 无法清理驱动程序目录**：在某些情况下，当你单击 "清除" 按钮时，权限错误可能会阻止 SDV 正确清除驱动程序目录中的旧结果。  如果以前运行的 sdv 文件当前正在使用中，则也会发生此错误。  确保未使用驱动程序目录中的 SDV 文件，并删除 "SDV" 和 "SDV" 文件夹以及任何 "staticdv" 文件。

如果 SDV 在尝试分析时失败，它会将失败的阶段打印到标准输出。  从 Visual Studio GUI 运行 SDV 时，可以通过切换到 "警报" 选项卡来查看此输出。

SDV 可能会失败的阶段包括：
* **NormalBuild**： SDV 无法使用标准 MSBuild 命令生成驱动程序。  如果你具有专门的生成逻辑、依赖你的项目文件中的解决方案元素或具有外部生成组件，则可能会发生这种情况。  如果你的项目依赖于 $ (SolutionDir) 属性，则可以通过从命令行重新运行 SDV 并将其追加到命令行来直接提供此变量，方法是在 MSBuild 命令的末尾添加 **/p： SolutionDir = \[ 你的 \] 解决方案目录**。  请参阅 [静态驱动程序验证程序命令 (MSBuild) ](-static-driver-verifier-commands--msbuild-.md)。
* **InterceptedBuild**： SDV 无法构建要分析的驱动程序。  
* **Scan**： SDV 找不到驱动程序的入口点。  此处的错误可能表示找不到入口点，应更新函数 roletypes 或 sdv。  有关详细信息，请参阅 [使用函数角色类型声明](using-function-role-type-declarations.md) 和 [批准 Sdv 文件](approving-the-sdv-map-h-file.md) 。
* **FinalCompile**： SDV 无法用规则和 OS 模型编译驱动程序。
* **CheckRule**： SDV 无法正确验证规则。

可以通过启用 SDV 诊断来了解有关错误的更多详细信息。  有关详细信息，请参阅 [静态驱动程序验证程序诊断](static-driver-verifier-diagnostics.md) 。
