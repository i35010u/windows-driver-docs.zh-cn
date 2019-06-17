---
title: 安全组命令
description: 以下各节介绍发送某些安全命令的特殊要求。
ms.assetid: 956C26D7-A434-4055-892B-E6E2D5B70CFA
ms.date: 06/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7838caeea32d418b710b0abf2639d4210ff3de9d
ms.sourcegitcommit: 19fbc6688128f31ce12bdc628c27ea0fa6cce79b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "67047047"
---
# <a name="security-group-commands"></a>安全组命令

此页描述发送某些 ATA 安全组命令的特殊要求。

**请注意**  中由 Microsoft 提供 ATA 存储驱动程序堆栈在 Windows Vista 和 Windows 7 中，允许任何 ATA 安全组命令。 在驱动程序初始化时阻止擦除发送安全冻结锁。

## <a name="secure-erase"></a>安全擦除

从 Windows 8 开始，发送 ATA 安全组的命令 （例如用来执行安全擦除命令） 的能力仅限于使用特定的硬编码密码与在 Windows 预安装环境 (WinPE)。

原因为这是为了确保，当发出安全擦除命令，设备可以保持处于安全状态时，在同一时间，允许在设备解锁如果安全擦除命令的处理过程中发生断电或其他不可预见的事件。

由于某些现有的应用程序仍需要发出以下命令，完成执行安全擦除的过程，使用此 ATA 安全组命令序列：

* 安全设置密码
* 准备安全擦除
* 安全擦除单元

若要执行安全擦除的要求如下：

* 安全冻结锁命令不会发送从 BIOS 在初始化过程。
* AHCI 控制器不在 IDE ATA/模式下运行 (例如 Microsoft PATA 驱动程序， *atapi.sys*，必须管理控制器)。
* WinPE 系统必须启动到 Windows 8 或更高版本的基于的。 在处于 WinPE 中 Microsoft 的 AHCI 驱动程序下, 运行时*StorAHCI.sys*，不会在初始化期间发送安全冻结锁定命令。
* 发出安全设置密码命令包含"AutoATAWindowsString12345678901"为用户密码字符串。 **注意：** 此命令允许设置仅在用户密码。
* 执行的必要时，安全命令处理包括发送安全擦除准备和安全擦除单元。

新的应用程序应使用的净化功能集 （也限制为 Windows 8 或更高版本的基于 WinPE） 中的加密 SCRAMBLE EXT 命令。 这是首选对安全擦除单元命令由于 T10 标准 (SCSI) 和 T13 标准 (ATA) 中以及所有派生总线支持净化。
