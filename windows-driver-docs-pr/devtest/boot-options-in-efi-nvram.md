---
title: EFI NVRAM 中的启动选项
description: 具有可扩展固件接口 (EFI 的计算机在 NVRAM 中) 固件存储启动选项，但即使关闭计算机，也会保留其状态。
keywords:
- NVRAM 启动选项 WDK
- EFI NVRAM 启动选项 WDK
- 启动选项 WDK，EFI NVRAM
- 可扩展固件接口 WDK 启动选项
- Itanium 处理器启动选项 WDK
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 997e39ac978450b55732183e096e943c4c8a23c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833571"
---
# <a name="boot-options-in-efi-nvram"></a>EFI NVRAM 中的启动选项


> [!IMPORTANT] 
> 本主题介绍 Windows XP 和 Windows Server 2003 中支持的启动选项。 如果要更改 Windows 的新式版本的启动选项，请参阅 [windows 中的 "启动选项](boot-options-in-windows.md)"。

具有可扩展固件接口的计算机 (EFI) 固件，如 Intel 安腾2处理器、在 NVRAM 中存储启动选项、可以编辑的存储介质，但即使关闭计算机也会保留其状态。 EFI 固件与 BIOS 固件的作用相同，但它克服了传统 BIOS 的许多限制。 在 BIOS 和启动管理器中实现的启动函数在基于 x86 的系统上 (NTLDR) 由 EFI 组件（即 EFI BIOS 和 EFI 启动管理器）处理。

若要在运行 Windows XP、Windows Server 2003 及其前置任务的基于 EFI 的系统上配置与驱动程序调试和测试相关的功能，必须在 NVRAM 中编辑启动选项。 以下部分简要介绍了 EFI NVRAM 中的启动选项，并说明了特定于使用此技术的系统的启动选项的各个方面。

在 Windows Vista 和更高版本的 Windows 上，基于 BIOS 和 EFI 的计算机上的启动选项存储在 *引导配置数据* (BCD) ，这是一个独立于固件的配置和存储系统，用于启动选项。 有关详细信息，请参阅 [Windows Vista 和更高版本中的启动选项](./boot-options-in-windows.md)。

有关基于 Itanium 的系统上的启动选项的详细说明，请参阅可扩展固件接口规范。 可以从 [Intel 可扩展固件接口](https://www.intel.com/content/www/us/en/architecture-and-technology/unified-extensible-firmware-interface/efi-homepage-general-technology.html) 网站下载更新的规范的副本。

本节包括：

- [EFI 中的启动选项概述](overview-of-boot-options-in-efi.md)
- [编辑 EFI 中的启动选项](editing-boot-options-in-efi.md)
- [备份 EFI 中的启动选项](backing-up-boot-options-in-efi.md)
