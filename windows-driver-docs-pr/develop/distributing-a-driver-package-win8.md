---
ms.assetid: 602bf657-7ae4-4610-b4c0-9d7260c42063
title: 分发驱动程序包
description: 分发驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1324c5771328a6a121554d1a4aa4bf803b09051a
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "64368619"
---
# <a name="distributing-a-driver-package"></a>分发驱动程序包

## <span id="ddk_distributing_a_driver_pg"></span><span id="DDK_DISTRIBUTING_A_DRIVER_PG"></span>


本主题介绍如何安全地分发驱动程序包。 此信息包括如何通过 Microsoft Windows 更新计划分发驱动程序包。 本主题还介绍了 Windows 如何保护系统文件。

## <a name="span-idddkwindowsupdatepgspanspan-idddkwindowsupdatepgspanwindows-update"></a><span id="ddk_windows_update_pg"></span><span id="DDK_WINDOWS_UPDATE_PG"></span>Windows 更新


* 通过 [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) 测试的[驱动程序包](https://msdn.microsoft.com/Library/Windows/Hardware/Ff544840)可以由 WHQL 进行数字签名。 如果驱动程序包由 WHQL 进行数字签名，则可以通过 Windows 更新计划或其他 Microsoft 支持的分发机制来分发。

获取 WHQL 发布签名是 [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) 的一部分。 WHQL 发布签名包含经过数字签名的[目录文件](https://msdn.microsoft.com/Library/Windows/Hardware/Ff537872)。 数字签名不会更改你提交用于测试的驱动程序二进制文件或 INF 文件。

如果驱动程序包满足以下条件，则可以通过 Windows 更新计划分发驱动程序包：

-   通过 WHQL 测试程序，并且收到 [WHQL 发布签名](https://msdn.microsoft.com/Library/Windows/Hardware/Ff553976)。

-   有资格参加 Windows 认证计划。

-   满足其他要求：能够确保 Windows 更新可以为用户设备确定正确的驱动程序包，可以合法分发并且可以自动下载包。

由于 Windows 更新计划的要求会经常更新，因此应定期查看 [Windows 更新驱动程序发布](https://go.microsoft.com/fwlink/p/?linkid=8712)网站。

## <a name="span-idddkprotectionforsystemfilespgspanspan-idddkprotectionforsystemfilespgspanprotection-for-system-files"></a><span id="ddk_protection_for_system_files_pg"></span><span id="DDK_PROTECTION_FOR_SYSTEM_FILES_PG"></span>对系统文件的保护


Windows 文件保护 (WFP) 保护 Windows 操作系统文件，防止文件被替换为未知或不兼容的版本。

WFP 阻止程序替换关键的 Windows 系统文件。 程序不得覆盖这些文件，因为操作系统和其他程序要使用这些文件。 保护这些文件可以防止程序和操作系统出现问题。

WFP 保护的系统文件类型包括随操作系统提供的 .sys、.exe、.ocx 和 .dll 文件。

在 WHQL 测试期间，[**Signability**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089) 程序会检查驱动程序的 INF 文件以确保它不会尝试替换系统文件。 尝试替换系统文件的驱动程序包无法收到数字签名。 但是，驱动程序包可以包含供应商提供给 Microsoft，以随 Windows 2000 或更高版本的操作系统提供的更新文件版本。

有关 Windows 文件保护的其他信息，请参阅 Windows SDK 文档。

 

 





