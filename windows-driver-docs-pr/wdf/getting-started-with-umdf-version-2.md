---
title: UMDF 入门
description: 本部分介绍用户模式驱动程序框架 (UMDF) ，并详细介绍了 UMDF 版本1和2之间的差异。
ms.assetid: 2C4DAFA4-783C-4739-8D27-A417AC63B447
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb197b001183a991d9f7d12409df3e87ba3b3971
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190349"
---
# <a name="getting-started-with-umdf"></a>UMDF 入门


本部分介绍用户模式驱动程序框架 (UMDF) ，并详细介绍了 UMDF 版本1和2之间的差异。 它还提供有关 UMDF 的高级体系结构信息。 使用此部分来确定 UMDF 驱动程序是否适合你的需求，并决定要使用哪个 UMDF 版本。

Windows 驱动程序框架 (WDF) 包含 UMDF，这是一个用于创建用户模式驱动程序的框架。 与内核模式驱动程序框架一样 (KMDF) ，UMDF 提供了一个来自 WDM 的抽象层，处理大部分即插即用 (PnP) 和电源管理功能，并允许该驱动程序选择启用特定功能和事件处理。

在 Windows 8.1 的版本中，有两个主要版本的 UMDF：版本1和2。 UMDF 版本 1.11 (一个点十一) 是最新版本的 UMDF 版本1，是 UMDF 2 出现之前的最终版本。 有关显示完整版本信息和操作系统相关性的表，请参阅 [UMDF 版本历史记录](umdf-version-history.md)。

使用 UMDF 版本1编写驱动程序需要使用 COM 编程模型来编写 c + + 代码。 虽然 UMDF 版本1基于与 KMDF 相同的概念驱动程序编程模型，但 UMDF 1 采用不同组件实现了模型、设备驱动程序接口 (DDIs) 和数据结构。

与此相反，从 UMDF 版本2开始，你可以使用 C 编程语言编写一个 UMDF 驱动程序，该驱动程序调用了可用于 KMDF 驱动程序的多种方法。 在 UMDF 版本2和 KMDF 之间共享的所有接口都具有相同的名称、参数和结构定义。 如果驱动程序只使用共享的功能，或在仅在一个框架中支持的调用周围使用条件宏，则可以编写一个可使用 UMDF 或 KMDF 编译的驱动程序。 有关详细信息，请参阅 [如何从 KMDF 驱动程序生成 UMDF 驱动程序](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)。

虽然 UMDF 2 与 KMDF 之间存在重大的通用性，但仍有一小部分功能只能在一个框架中使用。 有关详细信息，请参阅 [将 UMDF 2 功能与 KMDF 进行比较](comparing-umdf-2-0-functionality-to-kmdf.md)。 有关所有 UMDF 2 和 KMDF 回调和方法的列表以及它们适用于) 哪些框架 (，请参阅 [WDF 回调和方法摘要](/windows-hardware/drivers/ddi/_wdf/)。 在少数情况下，方法的结构成员或参数仅适用于一个框架或另一个框架。 文档介绍了相应参考页上的这些差异。

您必须选择其中一个;不能编写从 UMDF 版本1和2调用方法的 UMDF 驱动程序。

UMDF 版本2驱动程序仅在 Windows 8.1 或更高版本上运行。 如果需要编写在早于 Windows 8.1 的操作系统上运行的 UMDF 驱动程序，则需要写入 UMDF 1.x 驱动程序。 你可以使用版本1.11 来构建在 Windows Vista 和更高版本上运行的驱动程序。 有关版本1的详细信息，请参阅 [UMDF 1.X 设计指南](user-mode-driver-framework-design-guide.md)。 本部分介绍了 UMDF 版本2。



 

