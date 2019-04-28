---
title: 修复了 ComBuffer 和 Windows SMM 安全缓解表 (WSMT)
description: 修复了 ComBuffer 和 Windows SMM 安全缓解表 (WSMT)
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1b573858b60ced40ee8ae2c7e8f302389fabe440
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337614"
---
# <a name="fixed-combuffer-and-windows-smm-security-mitigation-table-wsmt"></a>修复了 ComBuffer 和 Windows SMM 安全缓解表 (WSMT)


Windows SMM 安全缓解表 (WSMT) 是包含标志，用于指明特定的安全功能已经在系统上的 ACPI 命名空间中所述的静态表。

保护标志字段指示存在系统固件中的特定 BIOS 安全缓解措施。 受支持的版本的 Windows 操作系统早期在初始化期间，以前的 ACPI 解释器启动 Windows SMM 安全表中读取。 Windows 操作系统可以选择启用、 禁用或取消功能根据这些 SMM 保护标志存在某些安全功能。

保护标志固定\_COMM\_缓冲区和通信\_缓冲区\_嵌套\_PTR\_保护依赖固件供应商重新设计系统管理中断 (SMIs) 权限仅读取或写入到包括 MMIO 和 EFI 分配内存的区域的"允许"列表。  不足够，若要检查的指针是 SMM 之外，它们必须仅为这些"安全"区域。  这可以防止 SMM 变得混淆的 deputy，这可以绕过 Windows 旗舰"防护"功能。 上面提到的保护标志仅引用输入的验证和检查，指针和当前不需要强制通过 SMM 页保护。

WSMT 支持以下版本的 Windows 中包括：

-   Windows Server Technical Preview 2016

-   Windows 10 版本 1607

-   Windows 10 版本 1703

## <a name="related-resources"></a>相关资源

[Windows SMM 安全缓解措施表 (WSMT)](https://go.microsoft.com/fwlink/p/?LinkId=786943)


