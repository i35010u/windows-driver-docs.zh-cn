---
title: 可以移植的具体驱动程序以及移植位置
description: 本主题介绍了哪些 WDM 驱动程序可以移植到 Windows 驱动程序框架（WDF），以及如何决定是移植到内核模式驱动程序框架（KMDF）还是用户模式驱动程序框架（UMDF）。
ms.assetid: 53E34B9C-8C0A-4F15-951B-7AB133DE0C5A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e85cdca164a1ee217e38ada5fe286620715a104
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842789"
---
# <a name="which-drivers-can-be-ported-and-where"></a>可以移植的具体驱动程序以及移植位置


本主题介绍了哪些 WDM 驱动程序可以移植到 Windows 驱动程序框架（WDF），以及如何决定是移植到内核模式驱动程序框架（KMDF）还是用户模式驱动程序框架（UMDF）。

## <a name="which-wdm-drivers-can-i-port-to-wdf"></a>我可以将哪些 WDM 驱动程序移植到 WDF？


特定驱动程序是否可以移植到 WDF 取决于以下条件：

-   运行驱动程序的操作系统版本
-   驱动程序支持的设备类型
-   驱动程序使用的驱动程序模型

通常，可以使用 KMDF 或 UMDF 来编写符合 WDM 的驱动程序，提供主要 i/o 调度例程的入口点，并处理 Irp。

对于某些设备类型，系统提供的设备类和端口驱动程序提供驱动程序调度功能并调用供应商提供的微型端口驱动程序来处理特定 i/o 详细信息。 这些微型端口驱动程序本质上是回调库，不受 WDF 支持。 此外，WDF 不支持使用 Windows 图像获取（WIA）的设备类型。

您可以使用 KMDF 创建在 Windows 2000 和更高版本上运行的驱动程序。 你可以使用 UMDF 版本1来编写在 Windows XP 及更高版本上运行的驱动程序，并使用 UMDF 版本2来 Windows 8.1 和更高版本。

有关 UMDF 和 KMDF 支持的设备和驱动程序类型的信息，请参阅[选择驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)。

## <a name="which-framework-should-i-port-my-wdm-driver-to-kmdf-or-umdf-2"></a>我应该将 WDM 驱动程序移植到哪个框架，KMDF 或 UMDF 2？


1.  查看将[UMDF 2.0 功能与 KMDF 进行比较](comparing-umdf-2-0-functionality-to-kmdf.md)时仅限 KMDF 的功能的列表。 如果你的驱动程序不需要任何这些功能，并且你面向 Windows 8.1 或更高版本，请在 Visual Studio 中打开新的 UMDF 2 驱动程序模板。

    如果以后需要 KMDF 的功能，可以直接将 UMDF 2 驱动程序转换为 KMDF，如[如何将 KMDF 驱动程序转换为 UMDF 2.0 驱动程序中所述（反之亦然）](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)。

2.  您还可以编写一个*模式无关*的驱动程序，这意味着可以使用 KMDF 或 UMDF 编译该驱动程序。 若要编写模式无关的驱动程序，请从 UMDF 2 模板开始。 使用[WDF 回调和方法摘要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)中列出的 DDI 版本信息，以确保仅调用 KMDF 和 UMDF 2 中可用的方法。 有条件[地使用如何将 KMDF 驱动程序转换为 UMDF 2.0 驱动程序](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)中所述的预处理器宏来标记任何标头引用（反之亦然）。 若要切换驱动程序，请使用适用于目标框架的 Visual Studio 模板创建一个空的驱动程序项目，并复制你的源代码。

## <a name="related-topics"></a>相关主题


[UMDF 入门](https://docs.microsoft.com/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)

[KMDF 版本历史记录](kmdf-version-history.md)

[UMDF 版本历史记录](umdf-version-history.md)

[用户模式 Driver Framework 常见问题](user-mode-driver-framework-frequently-asked-questions.md)

 

 






