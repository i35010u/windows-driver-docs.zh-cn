---
title: 在 64 位驱动程序支持 32 位 I/O
description: 在 64 位驱动程序支持 32 位 I/O
ms.assetid: c024c74e-0b83-4f86-8370-8269cbf69c9a
keywords:
- 32 位 I/O 支持 WDK 64 位
- 64 位 WDK 内核，32 位 I/O 支持
- 形式转换 WDK
- WOW64 形式转换层 WDK
- 将参数转换为固定精度的类型
- 32 位 I/O 有关 32 位 I/O 支持在 64 位支持 WDK 64 位
- 控制代码 WDK 64 位
- I/O 控制代码 WDK 内核，在 64 位驱动程序中的 32 位 I/O
- Ioctl WDK 内核，在 64 位驱动程序中的 32 位 I/O
- 文件系统控制代码 WDK 64 位
- FSCTL WDK 64 位
- 缓冲区指针 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b406413798edea839afee76c89600eea0bc46c9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556183"
---
# <a name="supporting-32-bit-io-in-your-64-bit-driver"></a>在 64 位驱动程序支持 32 位 I/O





Windows (WOW64) 上的 Windows 允许 Microsoft Win32 用户模式应用程序在 64 位 Windows 上运行。 通过截获 Win32 函数调用和参数从指针精度类型转换为固定精度类型作为相应地对 64 位内核转换之前执行此操作。 此转换称为*形式转换*，为所有 Win32 函数，但有一个重要的例外自动完成： 数据缓冲区传递给[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216). 通过指向这些缓冲区的内容*InputBuffer*并*OutputBuffer*不 thunked 参数，因为其结构是特定于驱动程序。

**请注意**  尽管缓冲区*内容*不 thunked 缓冲区*指针*转换为 64 位指针。

 

用户模式应用程序调用[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)将 I/O 请求直接发送到指定的内核模式驱动程序。 此请求包含 I/O 控制代码 (IOCTL) 或文件系统的控制代码 (FSCTL) 和指针的输入和输出数据缓冲区。 这些数据缓冲区的格式是特定于 IOCTL 或 FSCTL，反过来由内核模式驱动程序定义。 因为缓冲区格式是任意的而且它已知的驱动程序和不 WOW64 的形式转换数据任务由驱动程序。

如果满足以下所有 64 位驱动程序必须都支持 32 位 I/O:

-   该驱动程序向用户模式应用程序公开 IOCTL （或 FSCTL）。

-   至少一个使用 IOCTL 的 I/O 缓冲区包含指针精度数据类型。

-   IOCTL 代码轻松地不能重写以避免使用指针精确度缓冲区的数据类型。

 

 




