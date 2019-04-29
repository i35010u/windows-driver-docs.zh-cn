---
title: 安全组命令
description: 以下各节介绍发送某些安全命令的特殊要求。
ms.assetid: 956C26D7-A434-4055-892B-E6E2D5B70CFA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09af94c3f30b6d3f4253d95494a55edd29ad2998
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387940"
---
# <a name="security-group-commands"></a>安全组命令


以下各节介绍发送某些安全命令的特殊要求。

## <a name="span-idsecureerasespanspan-idsecureerasespansecure-erase"></a><span id="SECURE_ERASE"></span><span id="secure_erase"></span>安全擦除


若要提高数据安全性，从 Windows 8 开始发送 ATA 安全组的命令 （例如用来执行安全擦除命令） 的能力仅限于使用特定的硬编码密码与在 Windows 预安装环境 (WinPE)。 原因为这是为了确保，当发出安全擦除命令，设备可以保持处于安全状态时，在同一时间，允许在设备解锁如果安全擦除命令的处理过程中发生断电或其他不可预见的事件。

因为某些应用程序仍需要发出以下命令，介绍了执行安全擦除在 Windows 8 或更高版本的以下过程。

**请注意**  在 Windows Vista 和 Windows 7 没有 ATA 安全组命令允许在 microsoft 提供 ATA 存储驱动程序堆栈。 在驱动程序初始化时阻止擦除发送安全冻结锁。

 

使用这一序列的以下 ATA 安全组命令来执行安全擦除功能：

-   安全设置密码
-   准备安全擦除
-   安全擦除单元

若要执行安全擦除的要求如下：

-   安全冻结锁命令不会发送从 BIOS 在初始化过程。
-   AHCI 控制器不在 IDE ATA/模式下运行 (例如 Microsoft PATA 驱动程序， *atapi.sys*，必须管理控制器)。
-   系统必须引导至 Windows 8 或更高版本，其基于 WinPE。 在处于 WinPE 中 Microsoft 的 AHCI 驱动程序下, 运行时*StorAHCI.sys*，不会在初始化期间发送安全冻结锁定命令。
-   发出安全设置密码命令包含"AutoATAWindowsString12345678901"为用户密码字符串。

    **请注意**  此命令允许设置仅在用户密码。

     

-   执行的必要时，安全命令处理包括发送安全擦除准备和安全擦除单元。

对于新应用程序，建议使用加密 SCRAMBLE EXT 命令从净化功能集。 这是首选对安全擦除单元命令由于 T10 标准 (SCSI) 和 T13 标准 (ATA) 中以及所有派生总线支持净化。

 

 




