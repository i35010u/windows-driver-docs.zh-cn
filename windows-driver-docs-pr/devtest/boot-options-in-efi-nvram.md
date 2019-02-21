---
title: EFI NVRAM 中的启动选项
description: 即使在关闭计算机时，具有可扩展固件接口 (EFI) 固件存储启动选项 NVRAM 中的计算机但保留其状态。
ms.assetid: 99247d03-1723-4a2b-8ef4-c1f39687642f
keywords:
- NVRAM 启动选项 WDK
- EFI NVRAM 启动选项 WDK
- 启动选项 WDK、 EFI NVRAM
- 可扩展固件接口 WDK 启动选项
- Itanium 处理器启动选项 WDK
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: abeb2d396114f1e244215f200846eeb9ecdf5602
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555081"
---
# <a name="boot-options-in-efi-nvram"></a>EFI NVRAM 中的启动选项


> [!IMPORTANT] 
> 本主题介绍支持 Windows XP 和 Windows Server 2003 中的启动选项。 如果要更改的最新版本的 Windows 启动选项，请参阅[Windows Vista 和更高版本中的启动选项](boot-options-in-windows-vista-and-later.md)。

使用可扩展固件接口 (EFI) 固件，如 Intel Itanium 2 处理器的计算机将启动选项存储在 NVRAM，存储介质，可以编辑，但会保留其状态，即使关闭计算机。 EFI 固件的作用相同 BIOS 固件，但它克服了传统 BIOS 的很多限制。 EFI 组件 （即 EFI BIOS 和 EFI 启动管理器） 来处理在 BIOS 和启动管理器 (NTLDR) 中实现基于 x86 的系统的启动函数。

若要配置与调试和测试在运行 Windows XP、 Windows Server 2003 和早期版本的基于 EFI 的系统上的驱动程序相关的功能，必须编辑 NVRAM 中的启动选项。 以下各节简要描述 EFI NVRAM 中的启动选项，并解释特定于使用此技术的系统的启动选项的方面。

在 Windows Vista 和更高版本的 Windows 中，基于 BIOS 的和基于 EFI 的计算机上的启动选项存储在*引导配置数据*(BCD) 不依赖固件的配置和存储系统，用于启动选项。 有关详细信息，请参阅[Windows Vista 和更高版本中的启动选项](boot-options-in-windows-vista-and-later.md)。

有关在基于 Itanium 的系统上的启动选项的详细说明，请参阅可扩展固件接口规范。 可以下载一份从更新的规范[Intel 可扩展固件接口](https://go.microsoft.com/fwlink/p/?linkid=10596)网站。

本部分包括：

- [在 EFI 启动选项的概述](overview-of-boot-options-in-efi.md)
- [编辑在 EFI 启动选项](editing-boot-options-in-efi.md)
- [备份在 EFI 启动选项](backing-up-boot-options-in-efi.md)
