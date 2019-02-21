---
title: 在 Windows 中的启动选项的概述
description: 介绍 Windows 启动加载程序体系结构、 不依赖固件的启动配置和编辑工具的启动选项。
ms.assetid: 1cc5b1cc-8d0e-4b4e-93fe-272772a3e458
keywords:
- 启动选项 WDK，Windows
- 编辑启动选项
- 多重引导系统 WDK 启动选项
- 旧的启动项 WDK
- 启动配置数据 WDK
- BCD WDK
- BCDEdit 工具
- 启动选项 WDK，编辑
- ntldr 工具
- Windows 启动管理器 WDK
- Bootmgr 工具
- 特定于系统的引导加载程序 WDK
- 启动加载程序 WDK
- 不依赖固件的启动选项 WDK
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3a3933ccd6338d05d2774e9767b67a74b03c79f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526389"
---
# <a name="overview-of-boot-options-in-windows"></a>在 Windows 中的启动选项的概述

Windows 启动加载程序体系结构包括名为不依赖固件的引导配置和存储系统*引导配置数据*(BCD) 和启动选项编辑工具 BCDEdit (BCDEdit.exe)。 在开发期间，可以使用 BCDEdit 来配置用于调试、 测试和故障排除您运行 Windows 10、 Windows 8、 Windows Server 2012、 Windows 7 和 Windows Server 2008 的计算机上的驱动程序的启动选项。

> [!IMPORTANT] 
> 若要使用 BCDEdit 修改 BCD，所需管理权限。 更改使用 BCDEdit 某些启动项选项可能导致您的计算机无法运行。 或者，使用系统配置实用程序 (MSConfig.exe) 更改启动设置。

## <a name="boot-loading-architecture"></a>启动加载体系结构

Windows 包括旨在快速、 安全地加载 Windows 启动加载程序组件。 以前的 Windows NT 启动加载器*ntldr*，将替换为三个组件：

-   Windows 启动管理器 (Bootmgr.exe)

-   Windows 操作系统加载器 (Winload.exe)

-   Windows 恢复 (Winresume.exe) 加载程序

在此配置中，Windows 启动管理器是泛型和不识别实例的每个操作系统的特定要求而特定于系统的引导加载程序加载的系统进行了优化。

如果具有多个启动项的计算机的 Windows 包含至少一个条目，所在的根目录中，将 Windows 启动管理器启动系统，并与用户交互。 它显示启动菜单中，将加载所选的特定于系统的启动加载程序，并将引导参数传递给启动加载程序。

每个 Windows 分区的根目录中驻留的引导加载程序。 选择后，启动加载程序接管引导过程并加载操作系统根据选择的启动参数。

## <a name="boot-configuration-data"></a>启动配置数据

存储 Windows 启动选项基于 BIOS 的和基于 EFI 的计算机上的启动配置数据 (BCD) 存储中。

BCD 将传统的 Boot.ini 文本文件替换基于 BIOS 的系统中。 将启动参数存储在文本文件中，但是简单，被认为是太容易受到恶意攻击，以证明它的使用。 基于 EFI 的计算机上，启动选项的存储位置 NVRAM 中，使用相同的 BCD 方法编辑启动选项，像使用的基于 BIOS 的计算机上，而不是访问 NVRAM 直接使用 Windows Api 或专用的工具。

BCD 运行 Windows 10、 Windows 8、 Windows Server 2012、 Windows 7 和 Windows Server 2008 的所有计算机提供常见的、 不依赖固件的启动选项接口。 它是比以前的启动选项存储配置，更安全的因为它允许安全锁定 BCD 存储并可让管理员分配管理启动选项的权限。 在运行时并且在安装程序的所有阶段，BCD 才可用。 您甚至可以在电源状态转换期间调用 BCD 并使用它来定义后休眠状态恢复的启动过程。

您可以远程管理 BCD 时和管理 BCD 系统 BCD 存储所驻留的媒体以外的介质中启动。 此功能是非常重要的调试和故障排除，尤其是当 BCD 存储必须还原从 CD、 运行启动修复时从基于 USB 的存储媒体，或甚至远程。

BCD 是易于使用。 BCD 存储中，使用其熟悉的对象元素体系结构，使用 Guid 来精确地标识与启动相关应用程序。

BCD 包含其自己的启动选项集。 大部分 Windows 启动选项前所使用 BCD 时，如 **/debug**， **/maxmem**，并 **/pae**，都已被保留; 但是，在某些情况下，选项的名称可能已更改为更好地满足其功能。 详细了解这些启动选项，请参阅[BCD 启动选项参考](https://msdn.microsoft.com/library/windows/hardware/ff542205)。

## <a name="multiboot-scenarios"></a>多重引导方案

如果在计算机上安装了多个 Windows 操作系统，Windows 启动管理器适用于较旧的 （"传统"） 版本的 Windows 用户进行交互并启动所选的操作系统的启动组件。

多重引导计算机启动时，将出现下列情况：

-   Windows 启动管理器显示一个菜单，其中包含 Windows 的启动项的以及**旧版**选项。

-   如果选择特定版本的 Windows 的启动项，Windows 启动管理器加载特定于系统的引导加载程序为此操作系统，并将该启动项的参数传递到特定于系统的启动加载程序。 特定于系统的启动加载程序加载的启动参数，根据操作系统。

-   如果选择**旧版**，Windows 启动管理器启动 Ntldr，Windows Vista 之前的基于 NT 的 Windows 操作系统的启动管理器。 从这一刻起，启动过程将继续像以前那样在 Windows Vista 之前。

    如果计算机包含多个安装的早于 Windows Vista Windows，Ntldr 显示包含这些操作系统的条目启动菜单。 基于 BIOS 的系统上的 Boot.ini 文件中的条目和 EFI NVRAM 中存储在基于 EFI 的系统上的启动项生成此启动菜单。 当你选择的启动项时，Ntldr 加载的启动参数，根据操作系统。

## <a name="editing-boot-options"></a>编辑启动选项

若要编辑启动选项在 Windows 中的，使用 BCDEdit (BCDEdit.exe)，在 Windows 中包含的工具。 您不能用于 Bootcfg 或 NvrBoot 编辑启动选项中 Windows，但可继续使用它们来编辑在旧版本的 Windows 上的启动选项。

若要使用 BCDEdit，您必须在计算机上 Administrators 组的成员。

系统配置实用程序 (MSConfig.exe) 还可用于更改启动设置。

若要更改启动选项以编程方式在 Windows 中的，使用启动选项的 Windows 管理检测 (WMI) 接口。 此 BCD WMI 接口是最好的方法以编程方式更改启动选项。 关于 BCD WMI 界面的信息，请参阅[引导配置数据 WMI 提供程序](https://msdn.microsoft.com/library/windows/desktop/bb986746(v=vs.85).aspx)Windows SDK 文档中。

## <a name="related-topics"></a>相关主题

- [BCD Edit 选项引用](bcd-boot-options-reference.md)
- [编辑启动选项](editing-boot-options.md)
- [使用引导参数](using-boot-parameters.md)
- [启动配置数据](https://go.microsoft.com/fwlink/p/?linkid=74322)

