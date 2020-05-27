---
title: 修复了 ComBuffer 和 Windows SMM 安全缓解表 (WSMT)
description: 修复了 ComBuffer 和 Windows SMM 安全缓解表 (WSMT)
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: dafaa17592ad7878e9c011c4f005fc87e0731ad6
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851965"
---
# <a name="fixed-combuffer-and-windows-smm-security-mitigation-table-wsmt"></a>修复了 ComBuffer 和 Windows SMM 安全缓解表 (WSMT)

Windows SMM 安全缓解表（WSMT）是 ACPI 命名空间中所述的一个静态表，其中包含的标志表明已在系统上实现了特定的安全功能。

"保护标志" 字段指示系统固件中是否存在特定的 BIOS 安全缓解措施。 在启动 ACPI 解释器之前，Windows 操作系统支持的 Windows 操作系统版本在 Windows SMM 安全表中及早读取。 Windows 操作系统可能会根据这些 SMM 保护标志的存在，选择启用、禁用或取消功能特定的安全功能。

保护标志固定 \_ \_ 的通信缓冲区和 \_ comm \_ 缓冲 \_ 嵌套 \_ 的 PTR 保护依赖于固件供应商重新设计系统管理中断（SMIs），以便仅读取或写入包含 MMIO 和 EFI 分配内存的区域的 "允许" 列表。不能检查指针是否在 SMM 之外，它们必须仅在这些 "安全" 区域内。这可以防止 SMM 成为一种困惑的 deputy，它可以绕过 Windows 旗舰 "Guard" 功能。 上面提到的保护标志仅引用输入验证和指针检查，当前不需要通过 SMM 页保护进行强制。

以下 Windows 版本中包含对 WSMT 的支持：

- Windows Server Technical Preview 2016

- Windows 10 版本 1607

- Windows 10 版本 1703

## <a name="related-resources"></a>相关资源

[Windows SMM 安全缓解表（WSMT）](https://go.microsoft.com/fwlink/p/?LinkId=786943)
