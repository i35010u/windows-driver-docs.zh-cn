---
title: 设置调试（内核模式和用户模式）
description: 可以通过两种方式设置 Windows 调试器调试。
ms.assetid: 3575B850-A0F9-4AAE-9432-E970D40069D2
keywords:
- 安装程序调试
- 配置调试
- 配置调试器
- WinDbg
- Visual Studio 调试
- 内核模式调试
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2b458ffbd5dba5c45dfa61acd396b836fc555b42
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528961"
---
# <a name="setting-up-debugging-kernel-mode-and-user-mode"></a>设置调试（内核模式和用户模式）

设置内核模式调试后，可以使用 WinDbg 或 KD 建立调试会话。 设置用户模式调试后，可以使用 WinDbg、CDB 或 NTSD 建立调试会话。

**请注意**  windows 调试器包含在适用于 Windows 的调试工具中。 这些调试器不同于 visual studio 调试器，后者包含在 Visual Studio 中。 有关详细信息，请参阅[Windows 调试](index.md)。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容

### <a name="configuring-transports"></a>配置传输

- [设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

### <a name="supported-target-pc-nics"></a>支持的目标 PC Nic

- [Windows 10 中的网络内核调试支持的以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)
- [Windows 8.1 中用于网络内核调试的受支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)
- [Windows 8 中用于网络内核调试的受支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

### <a name="additional-configuration-tools"></a>其他配置工具

- [配置 tools .ini](configuring-tools-ini.md)
- [使用 KDbgCtrl](using-kdbgctrl.md)
