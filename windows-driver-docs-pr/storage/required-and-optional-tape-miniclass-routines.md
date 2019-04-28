---
title: 必需的和可选的磁带微型类例程
description: 必需的和可选的磁带微型类例程
ms.assetid: 7a641199-2607-4980-bd8b-ec3856b311ef
keywords:
- 磁带驱动程序 WDK 存储，可选的例程
- 存储磁带驱动程序 WDK，可选的例程
- 磁带驱动程序 WDK 存储，所需的例程
- 存储磁带驱动程序 WDK，所需的例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f50eae3803f9297bf157153ed563e3f1cbad0cf3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352631"
---
# <a name="required-and-optional-tape-miniclass-routines"></a>必需的和可选的磁带微型类例程


## <span id="ddk_required_and_optional_tape_miniclass_routines_kg"></span><span id="DDK_REQUIRED_AND_OPTIONAL_TAPE_MINICLASS_ROUTINES_KG"></span>


磁带 miniclass 驱动程序必须具有以下例程：

-   **DriverEntry**提供特定于驱动程序的入口点和磁带类驱动程序用于初始化 miniclass 驱动程序的常量。

    磁带 miniclass 驱动**DriverEntry**例程分配磁带\_INIT\_数据\_结构，例如设置特定于驱动程序常量和入口点在结构中，再调用**TapeClassInitialize**磁带类驱动程序中。

-   实现特定于设备的设备控制请求，如 TapeMiniGetPosition 和 TapeMiniGetMediaTypes 处理例程。

    磁带类驱动程序从其设备控制调度例程调用这样的例程。 有关详细信息，请参阅[处理磁带设备控制请求](processing-tape-device-control-requests.md)。

磁带 miniclass 驱动程序可以具有以下可选例程：

-   TapeMiniExtensionInit 初始化可选 minitape 扩展。

    请参阅[可选扩展中的存储磁带 Miniclass 上下文](storing-tape-miniclass-context-in-optional-extensions.md)minitape 扩展有关的信息。

-   TapeMiniTapeError 补充磁带类驱动程序的错误处理。

    对于大多数设备，磁带类驱动程序可以在实际应用而无需从盿 miniclass 驱动程序的输入发生错误时返回相应的状态值。 但是，对于某些设备，磁带类驱动程序要求从磁带 miniclass 驱动程序返回的相应状态的特定于设备的信息。 例如，4 毫米 DAT 磁带驱动器的 miniclass 驱动程序可以确定，在某些情况下，磁带\_状态\_总线\_重置状态实际是由于没有介质的驱动器中。 4 毫米 DAT miniclass 驱动程序的 TapeMiniTapeError 例程标识这些情况下，并返回到磁带的状态更改\_错误\_否\_媒体。

磁带 miniclass 驱动**DriverEntry**例程必须使用该名称完全才能由操作系统自动加载。 TapeMini*Xxx*例程可以命名为选择的驱动程序编写器，只要例程的入口点设置中将磁带\_INIT\_数据\_EX 结构。 若要帮助调试，miniclass 驱动程序应前缀 TapeMini*Xxx*例程使用某些字符来标识自身，并且应确保在名称中的字符的其余部分反映该例程的作用。

另请参阅中的磁带 miniclass 例程的说明[磁带 Miniclass 驱动程序例程](https://msdn.microsoft.com/library/windows/hardware/ff567970)。

 

 




