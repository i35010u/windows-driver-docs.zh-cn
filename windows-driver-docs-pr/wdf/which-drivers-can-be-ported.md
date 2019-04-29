---
title: 可以移植的具体驱动程序以及移植位置
description: 本主题介绍哪些 WDM 驱动程序可以移植到 Windows 驱动程序框架 (WDF)，以及如何决定是否要移植到内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF)。
ms.assetid: 53E34B9C-8C0A-4F15-951B-7AB133DE0C5A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3ac883eb29b1aac4d7069bba0db51c7c3a719c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385707"
---
# <a name="which-drivers-can-be-ported-and-where"></a>可以移植的具体驱动程序以及移植位置


本主题介绍哪些 WDM 驱动程序可以移植到 Windows 驱动程序框架 (WDF)，以及如何决定是否要移植到内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF)。

## <a name="which-wdm-drivers-can-i-port-to-wdf"></a>可移植到 WDF 的 WDM 驱动程序？


特定驱动程序是否可以移植到 WDF 取决于以下条件：

-   该驱动程序运行的操作系统版本
-   设备驱动程序支持的类型
-   该驱动程序使用的驱动程序模型

一般情况下，您可以到符合 WDM 的写入驱动程序使用 KMDF 或 UMDF，提供入口点的主要 I/O 调度例程，并处理 Irp。

对于某些设备类型，系统提供的设备类和端口驱动程序提供驱动程序调度函数和调用供应商提供的微型端口驱动程序来处理 I/O 的特定详细信息。 这些微型端口驱动程序是实质上是回调库和不受 WDF。 此外，WDF 不支持使用 Windows 图像采集 (WIA) 的设备类型。

KMDF 可用于创建运行 Windows 2000 及更高版本的驱动程序。 可以使用 UMDF 版本 1 编写运行 Windows XP 及更高版本，驱动程序和 UMDF 版本 2 到目标 Windows 8.1 及更高版本。

有关 UMDF 和 KMDF 支持的设备和驱动程序类型的信息，请参阅[选择驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff554652)。

## <a name="which-framework-should-i-port-my-wdm-driver-to-kmdf-or-umdf-2"></a>哪个框架应移植到 KMDF 或 UMDF 2 我 WDM 驱动程序？


1.  查看列表中的仅限 KMDF 的功能[将 UMDF 2.0 功能比较 KMDF](comparing-umdf-2-0-functionality-to-kmdf.md)。 如果您的驱动程序不需要其中的任何功能，以及面向 Windows 8.1 或更高版本，在 Visual Studio 中打开一个新的 UMDF 2 驱动程序模板。

    如果您以后意识到需要仅限 KMDF 的功能，它很简单明了将 UMDF 2 驱动程序转换为 KMDF，如中所述[如何将 KMDF 驱动程序转换到 UMDF 2.0 驱动程序 （以及进行相反转换）](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)。

2.  此外可以编写*模式下不可知*驱动程序，这意味着一个可以使用 KMDF 或 UMDF 编译。 若要编写不限模式的驱动程序，请使用 UMDF 2 模板开始。 使用 DDI 的版本控制信息中列出[WDF 回调摘要和方法](https://msdn.microsoft.com/library/windows/hardware/dn265591)以确保您只调用 KMDF 和 UMDF 2 中可用的方法。 有条件地标记标头的任何引用中所述的预处理器宏[如何将 KMDF 驱动程序转换到 UMDF 2.0 驱动程序 （以及进行相反转换）](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)。 若要切换您的驱动程序，会创建空的驱动程序项目的目标框架中，使用 Visual Studio 模板，并复制你的源代码。

## <a name="related-topics"></a>相关主题


[UMDF 入门](https://msdn.microsoft.com/library/windows/hardware/dn384105)

[KMDF 版本历史记录](kmdf-version-history.md)

[UMDF 版本历史记录](umdf-version-history.md)

[用户模式驱动程序框架方面的常见问题](user-mode-driver-framework-frequently-asked-questions.md)

 

 






