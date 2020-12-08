---
title: 设置调试（内核模式和用户模式）
description: 可以通过两种方式设置 Windows 调试器调试。
keywords:
- 安装程序调试
- 配置调试
- 配置调试器
- WinDbg
- Visual Studio 调试
- 内核模式调试
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9eb15060301429b1a44030e5dab826f817729ff9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816345"
---
# <a name="setting-up-debugging-kernel-mode-and-user-mode"></a>设置调试（内核模式和用户模式）

设置内核模式调试后，可以使用 WinDbg 或 KD 建立调试会话。 设置用户模式调试后，可以使用 WinDbg、CDB 或 NTSD 建立调试会话。

**注意**  Windows 调试器包含在 Windows 调试工具中。 这些调试器不同于 visual studio 调试器，后者包含在 Visual Studio 中。 有关详细信息，请参阅 [Windows 调试](index.md)。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容

### <a name="configuring-transports"></a>配置传输

- [设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

### <a name="supported-target-pc-nics"></a>支持的目标 PC Nic

- [Windows 10 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)
- [Windows 8.1 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)
- [Windows 8 中的网络内核调试支持的以太网 NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

### <a name="additional-configuration-tools"></a>其他配置工具

- [配置 tools.ini](configuring-tools-ini.md)
- [使用 KDbgCtrl](using-kdbgctrl.md)
