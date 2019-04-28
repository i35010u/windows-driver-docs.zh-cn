---
title: 安全启动
description: 安全启动
ms.date: 08/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0eb14f0dd0e396442b100b0a1c9e7636a976cb56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337386"
---
# <a name="secure-boot"></a>安全启动


安全启动是一个过程，以确保在 PC 启动使用受电脑制造商的软件。 安全启动不专用于 Microsoft，但 Microsoft 具有下面包含的链接中定义的特定要求，UEFI 规范文档中定义。

当启动 PC 时，固件检查启动软件，包括固件驱动程序 (选项 Rom) 和操作系统每段的签名。 如果签名是很好，PC 启动和固件将控制权交给操作系统。

安全启动是所必需的 Windows 操作系统;Windows 8、 8.1 和 10，并且也是 UEFI 规范文档的一部分。请参阅部分[27.1 安全启动](https://www.uefi.org/sites/default/files/resources/UEFI_2_3_1_C.pdf)在 UEFI 规范文档中的其他信息。

有关 Windows 安全启动的要求的详细信息，请参阅**System.Fundamentals.Firmware.UEFISecureBoot**中**WHCP 系统规范 1607年**下面的链接。

## <a name="related-resources"></a>相关资源

[硬件安全可测试性规范](https://docs.microsoft.com/windows-hardware/test/hlk/testref/hardware-security-testability-specification)

[Windows 硬件兼容性程序规范和策略](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)

[WHCP-Systems-Specification-1607](https://go.microsoft.com/fwlink/?linkid=866948)

[安全的引导和标准的引导：强化防止恶意软件的早期启动组件](https://msdn.microsoft.com/library/windows/hardware/dn653311)

[Windows 8.1 安全启动密钥创建和管理指南](https://technet.microsoft.com/library/dn747883)



