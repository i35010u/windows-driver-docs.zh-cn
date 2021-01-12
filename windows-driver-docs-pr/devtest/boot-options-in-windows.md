---
title: Windows 中的启动选项概述
description: 描述 Windows 启动加载器体系结构、独立于固件的启动配置和启动选项编辑工具。
keywords:
- 启动选项 WDK，Windows
- 编辑启动选项
- 多重引导系统 WDK 启动选项
- 旧启动条目 WDK
- 引导配置数据 WDK
- BCD WDK
- BCDEdit 工具
- 启动选项 WDK，编辑
- ntldr 工具
- Windows 启动管理器 WDK
- Bootmgr 工具
- 系统特定的启动加载程序 WDK
- 启动加载加载 WDK
- 独立于固件的启动选项 WDK
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5da3539eaab136e57c62efedee033f90a27c5166
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124271"
---
# <a name="overview-of-boot-options-in-windows"></a>Windows 中的启动选项概述

Windows 启动加载器体系结构包括与固件无关的启动配置和存储系统（称为 *引导配置数据* (BCD) 和启动选项编辑工具，BCDEdit ( # A0) 。 在开发过程中，您可以使用 BCDEdit 来配置用于在运行 Windows 10、Windows 8、Windows Server 2012、Windows 7 和 Windows Server 2008 的计算机上调试、测试和排查您的驱动程序的启动选项。

> [!CAUTION]
> 需要管理权限才能使用 BCDEdit 来修改 BCD。 使用 BCDEdit 更改某些启动项选项可能会导致计算机无法操作。 请改为使用系统配置实用程序 (MSConfig.exe) 更改启动设置。

## <a name="boot-loading-architecture"></a>启动加载体系结构

Windows 包括旨在快速、安全地加载 Windows 的启动加载程序组件。 以前的 Windows NT 启动加载程序 *ntldr* 由三个组件替代：

- Windows 启动管理器 ( # A0) 

- Windows 操作系统加载程序 ( # A0) 

- Windows 恢复加载器 ( # A0) 

在此配置中，Windows 启动管理器是通用的，并不知道每个操作系统的特定要求，而系统特定的启动加载程序会针对其加载的系统进行优化。

当具有多个启动条目的计算机至少包含一个 Windows 条目时，位于根目录中的 Windows 启动管理器将启动系统并与用户交互。 它显示启动菜单，加载所选的特定于系统的启动加载程序，并将引导参数传递到启动加载程序。

启动加载加载项位于每个 Windows 分区的根目录中。 选择后，启动加载程序将接管启动过程，并根据所选的启动参数加载操作系统。

## <a name="boot-configuration-data"></a>引导配置数据

Windows 启动选项存储在基于 BIOS 和 EFI 的计算机上引导配置数据 (BCD) 存储区中。


BCD 为运行 Windows 10、Windows 8、Windows Server 2012、Windows 7 和 Windows Server 2008 的所有计算机提供与固件无关的通用启动选项接口。 它比以前的启动选项存储配置更安全，因为它允许安全锁定 BCD 存储，并允许管理员分配管理启动选项的权限。 在运行时以及在安装程序的所有阶段都可以使用 BCD。 甚至可以在电源状态转换期间调用 BCD，并使用它定义启动过程以在休眠后恢复。

可以远程管理 BCD，并在系统从其他介质（而不是 BCD 存储所在的介质）启动时管理 BCD。 此功能对于调试和故障排除非常重要，尤其是在从 DVD 运行启动修复、从基于 USB 的存储媒体，甚至远程时，必须还原 BCD 存储。

具有熟悉的对象和元素体系结构的 BCD 存储使用 Guid 和名称（如 "Default"）来精确标识与启动相关的应用程序。

BCD 包含自己的一组启动选项。 有关这些启动选项的详细信息，请参阅 [BCD 启动选项参考](./bcd-boot-options-reference.md)。

## <a name="editing-boot-options"></a>编辑启动选项

若要在 Windows 中编辑启动选项，请使用 BCDEdit ( # A0) ，它是 Windows 中包含的工具。 

若要使用 BCDEdit，你必须是计算机上 Administrators 组的成员。

你还可以使用系统配置实用工具 ( # A0) 更改启动设置。

若要在 Windows 中以编程方式更改启动选项，请使用 Windows Management 检测 (WMI) 接口启动选项。 此 BCD WMI 接口是以编程方式更改启动选项的最佳方法。 有关 BCD WMI 接口的信息，请参阅 Windows SDK 文档中的 [引导配置数据 WMI 提供程序](/previous-versions/windows/desktop/bcd/boot-configuration-data-portal) 。

## <a name="related-topics"></a>相关主题

- [BCD 编辑选项参考](bcd-boot-options-reference.md)
- [编辑启动选项](editing-boot-options.md)
- [使用启动参数](using-boot-parameters.md)