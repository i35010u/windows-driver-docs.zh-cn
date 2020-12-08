---
title: 框架库版本控制
description: 在本主题中，你将了解 Kernel-Mode Driver Framework (KMDF) 库和 User-Mode 驱动程序框架 (UMDF) 库的文件名的命名约定。
keywords:
- 内核模式驱动程序 WDK KMDF，库版本
- KMDF WDK，库版本
- Kernel-Mode Driver Framework WDK，库版本
- 库 WDK KMDF
- 版本号 WDK KMDF
- 主要版本号 WDK KMDF
- 次版本号 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c3431cf429416ab24a5cd205b8010a56a1dcaba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815683"
---
# <a name="framework-library-versioning"></a>框架库版本控制


在本主题中，你将了解 Kernel-Mode Driver Framework (KMDF) 库和 User-Mode 驱动程序框架 (UMDF) 库的文件名的命名约定。

## <a name="kmdf"></a>KMDF


主版本号和次版本号将分配给每个版本的 KMDF 库。 库的文件名包含主要版本号。 文件名的格式为：

**Wdf** &lt;*MajorVersionNumber* &gt;**000.sys**

主要版本号使用两个字符。 例如，库1.0 版的文件名 *Wdf01000.sys*。 版本1.9、1.11 等也称为 *Wdf01000.sys*，而库文件的每个新的次要版本将覆盖文件的以前版本。

如果你使用比系统上的 framework 版本新的 KMDF 库版本构建驱动程序，则必须更新后一种版本。 有关更新框架库的信息，请参阅可 [再发行框架组件](installation-components-for-kmdf-drivers.md)。

 (请注意，框架共同安装程序的文件名同时包含主版本号和次版本号。 有关共同安装程序文件名的详细信息，请参阅 [使用 KMDF 共同安装程序](installing-the-framework-s-co-installer.md)。 ) 

构建驱动程序时，MSBuild 实用工具会将驱动程序与一个存根文件链接，其中包含 MSBuild 实用工具使用的库的版本号。 当操作系统加载你的驱动程序时，框架的加载程序将检查驱动程序存根中的版本信息，以确定驱动程序是否将与系统上的 framework 库版本一起运行。

若要确定驱动程序运行时所在的库版本，驱动程序可以调用 [**WdfDriverIsVersionAvailable**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverisversionavailable) 或 [**WdfDriverRetrieveVersionString**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverretrieveversionstring)。

WDF 允许使用不同于运行驱动程序的 Windows 版本来构建驱动程序。  有关详细信息，请参阅 [为多个版本的 Windows 构建 WDF 驱动程序](./building-a-wdf-driver-for-multiple-versions-of-windows.md)。

有关 KMDF 库的版本历史记录的信息，请参阅 [KMDF 版本历史记录](kmdf-version-history.md)。

## <a name="umdf"></a>UMDF


与 KMDF 一样，UMDF 库的主版本号使用两个字符。 但是，主版本号仅出现在 UMDF 库文件名称中，从版本2.0 开始。

对于 UMDF 版本2.0，将 *Wudfx02000.dll* umdf 库的文件名。

适用于 UMDF 版本1。*x*，将 *Wudfx.dll* UMDF 库的文件名。

有关 KMDF 库的版本历史记录的信息，请参阅 [UMDF 版本历史记录](umdf-version-history.md)。
