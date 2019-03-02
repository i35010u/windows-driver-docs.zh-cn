---
ms.assetid: 51CD05AB-2626-4E27-AA08-09547D546218
title: 将 WDK 8.1 项目转换为 WDK 10
description: 如何将使用 Microsoft Visual Studio 2013 和 Windows 驱动程序工具包 (WDK) 8.1 创建的驱动程序项目转换为在 Microsoft Visual Studio 2015 中使用 Windows 驱动程序工具包 (WDK) 10 生成的驱动程序项目。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d3fa096f10d2cfe3a6bc592c0c98f21317fd68b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518285"
---
# <a name="converting-wdk-81-projects-to-wdk-10"></a>将 WDK 8.1 项目转换为 WDK 10

本主题介绍如何将使用 Microsoft Visual Studio 2013 和 Windows 驱动程序工具包 (WDK) 8.1 创建的驱动程序项目转换为在 Microsoft Visual Studio 2015 中使用 Windows 驱动程序工具包 (WDK) 10 生成的驱动程序项目。

Visual Studio 2015 存在新的编译器警告和错误。 即使在 Visual Studio 2013 中生成驱动程序项目时没有出现任何错误，在 Visual Studio 2015 中生成该项目时也可能遇到错误。

请在驱动程序解决方案中使用以下步骤转换项目。

1.  在 Visual Studio 2015 中打开旧驱动程序解决方案。

    Visual Studio 会在此解决方案中自动运行 ProjectUpgradeTool 来转换项目。 也可以从命令行运行此工具。 默认情况下，安装 WDK 时，ProjectUpgradeTool.exe 会安装在 Windows Kits\\10\\bin\\x86 中。

    Visual Studio 打开标题为“升级 VC++ 编译器和库”的“查看解决方案操作”对话框。 单击“确定”，Visual Studio 会尝试升级解决方案中的所有项目。

    如果显示“检测到文件修改”对话框，请选择“全部重新加载”。

2.  在“解决方案资源管理器”窗格中，右键单击驱动程序项目的名称，然后选择“属性”。 单击“配置管理器”按钮。 在“活动解决方案配置”列表中，选择“&lt;新建…&gt;”。 键入一个名称，然后从 Windows 8.1 项目上下文中复制设置。 单击“确定” 。

    通常，转换后的解决方案包含两个配置文件，一个用于调试（测试），另一个用于发布。 若要使用 WDK 10 创建类似环境，只需选择“&lt;新建…&gt;”两次。 若要创建调试配置文件，请从“Win 8.1 调试”配置文件复制。 若要创建发布配置文件，请从“Win 8.1 发布”配置文件复制。

3.  在 WDK 10 以前的 WDK 版本中，驱动程序解决方案始终需要包项目。 在 WDK 10 中，仅当在驱动程序包中加入多个驱动程序时才需要包项目。 使用以下指南：

    -   如果解决方案中只有一个驱动程序且存在包项目，请将其删除。

    -   如果解决方案中有多个驱动程序，请确保解决方案包含包项目。 然后，对于解决方案中的每个驱动程序项目，打开项目属性并导航到“配置属性”&gt;“驱动程序设置”。 将“生成包”设置为“否”。 如果从命令行生成，请设置 **/p:SupportsPackaging=false**。

4.  同样，在驱动程序项目属性中，选择“属性”。 导航到“配置属性”&gt;“驱动程序设置”&gt;“常规”&gt;“目标 OS 版本”。 选择“Windows 10”。

    确认“目标平台”设置为“桌面”，然后生成解决方案。 修复发生的任何错误。

5.  成功生成解决方案后，将“目标平台”更改为“通用”。

    再次生成解决方案。 此时，仅有的错误来自 ApiValidator 工具，该工具检查驱动程序是否调用非通用功能。 将对非通用 DDI 的任何调用全部替换为对通用 DDI 的调用。

    有关 ApiValidator 的详细信息，请参阅[验证通用 Windows 驱动程序](validating-universal-drivers.md)。

    若要了解如何确定给定 DDI 的目标平台，请参阅[驱动程序的目标平台的参考页面](windows-10-editions-for-universal-drivers.md)。

 

 





