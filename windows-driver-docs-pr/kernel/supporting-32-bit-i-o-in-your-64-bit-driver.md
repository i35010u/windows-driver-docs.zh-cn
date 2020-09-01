---
title: 在 64 位驱动程序中支持 32 位 I/O
description: 在 64 位驱动程序中支持 32 位 I/O
ms.assetid: c024c74e-0b83-4f86-8370-8269cbf69c9a
keywords:
- 32位 i/o 支持 WDK 64 位
- 64位 WDK 内核，32位 i/o 支持
- thunk WDK
- WOW64 thunk 层 WDK
- 将参数转换为固定精度类型
- 32位 i/o 支持 WDK 64 位，关于64位中的32位 i/o 支持
- 控制代码 WDK 64 位
- I/o 控制代码 WDK 内核，64位驱动程序中的32位 i/o
- IOCTLs WDK 内核，64位驱动程序中的32位 i/o
- 文件系统控制代码 WDK 64 位
- FSCTL WDK 64 位
- 缓冲区指针 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2560ebed872812a7dcfabcbceeda67931b2654c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185983"
---
# <a name="supporting-32-bit-io-in-your-64-bit-driver"></a>在 64 位驱动程序中支持 32 位 I/O





Windows 上的 windows (WOW64) 使 Microsoft Win32 用户模式应用程序可以在64位 Windows 上运行。 它通过以下方式来实现此过程：在转换到64位内核之前，截获 Win32 函数调用并将参数从指针精度类型转换为固定精度类型。 这称为 *thunk*的转换是为所有 Win32 函数自动完成的，但有一个重要的例外：传递到 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)的数据缓冲区。 这些缓冲区的内容由 *InputBuffer* 和 *OutputBuffer* 参数指向，因为它们的结构特定于驱动程序。

**注意**   尽管缓冲区*内容*不 thunked，但缓冲区*指针*会转换为64位指针。

 

用户模式应用程序调用 [**DeviceIoControl**](/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) ，将 i/o 请求直接发送到指定的内核模式驱动程序。 此请求包含 i/o 控制代码 (IOCTL) 或文件系统控制代码 (FSCTL) 和指向输入和输出数据缓冲区的指针。 这些数据缓冲区的格式特定于 IOCTL 或 FSCTL，后者又由内核模式驱动程序定义。 因为缓冲区格式是任意的，并且由于驱动程序（而不是 WOW64）知道该格式，所以 thunk 的任务会将数据保留到驱动程序中。

如果满足以下所有条件，则64位驱动程序必须支持32位 i/o：

-   驱动程序向用户模式应用程序公开 IOCTL (或 FSCTL) 。

-   IOCTL 使用的至少一个 i/o 缓冲区包含指针精度数据类型。

-   不能轻松地重写 IOCTL 代码以消除指针精度缓冲区数据类型的使用。

 

