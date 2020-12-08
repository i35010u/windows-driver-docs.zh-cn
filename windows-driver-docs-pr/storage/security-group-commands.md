---
title: 安全组命令
description: 以下各节描述了发送特定安全命令的特殊要求。
ms.date: 06/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 179b1d7a257c2e25c16a0eee38b51ecb5268a876
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839387"
---
# <a name="security-group-commands"></a>安全组命令

本页介绍发送某些 ATA 安全组命令的特殊要求。

**注意**  在 Windows Vista 和 Windows 7 中，不允许在 Microsoft 提供的 ATA 存储驱动程序堆栈中使用 ATA 安全组命令。 安全冻结锁定在驱动程序初始化时发送，阻止擦除。

## <a name="secure-erase"></a>安全清除

从 Windows 8 开始，能够发送 ATA 安全组命令 (例如，用于执行安全擦除) 的命令仅限于 Windows 预安装环境 (WinPE) 使用特定的硬编码的密码。

这样做的原因是为了确保在发出安全擦除命令时，设备可以保持安全状态，同时，如果在处理安全擦除命令的过程中出现断电或其他一些不可预见的事件，则允许设备解锁。

由于一些现有应用程序仍需要发出这些命令，因此使用此 ATA 安全组命令序列执行安全擦除的过程如下：

* 安全设置密码
* 安全清除准备
* 安全清除单元

执行安全擦除的要求包括：

* 在初始化期间，不会从 BIOS 发送安全冻结锁定命令。
* AHCI 控制器未在 IDE/ATA 模式下运行 (例如，Microsoft PATA 驱动程序（ *atapi.sys*）不得管理控制器) 。
* 系统必须启动到基于 Windows 8 或更高版本的 WinPE。 在 WinPE 下运行时，Microsoft 的 AHCI 驱动程序 *StorAHCI.sys*，在初始化过程中不会发送安全冻结锁定命令。
* 发出安全设置密码命令，其中包含 "AutoATAWindowsString12345678901" 作为用户密码字符串。 **注意：** 此命令允许仅设置用户密码。
* 根据需要执行安全命令处理，包括发送安全清除准备和安全擦除单元。

新应用程序应使用净化功能集中的加密编码扩展命令 (也限制为基于 Windows 8 或更高版本的 WinPE) 。 这优先于 SECURITY ERASE 单元命令，因为 T10 标准 (SCSI) 和 T13 standard (ATA) 以及所有派生总线都支持净化。
