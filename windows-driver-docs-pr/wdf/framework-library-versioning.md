---
title: 框架库版本控制
description: 在本主题中，您将了解内核模式驱动程序框架 (KMDF) 库和用户模式驱动程序框架 (UMDF) 库的文件名称的命名约定。
ms.assetid: 51db6f3c-45cb-46a7-9dd4-2bab67893fea
keywords:
- 内核模式驱动程序 WDK KMDF，库版本
- KMDF WDK，库版本
- 内核模式驱动程序框架 WDK，库版本
- 库 WDK KMDF
- 版本号 WDK KMDF
- 主要版本号 WDK KMDF
- 次要版本号 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a9d811cfbc8d50d856e186c99abc120045617c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384464"
---
# <a name="framework-library-versioning"></a>框架库版本控制


在本主题中，您将了解内核模式驱动程序框架 (KMDF) 库和用户模式驱动程序框架 (UMDF) 库的文件名称的命名约定。

## <a name="kmdf"></a>KMDF


主版本号和次版本号已分配给 KMDF 库的每个版本。 库的文件名称中包含的主版本号。 将文件名称的格式为：

**Wdf**&lt;*MajorVersionNumber*&gt;**000.sys**

主版本号使用两个字符。 例如，对于 1.0 版的库文件名称是*Wdf01000.sys*。 版本 1.9、 1.11 等也称为*Wdf01000.sys*，和库文件的每个新次要版本将覆盖以前版本的文件。

如果生成您使用的系统上的 framework 版本比新 KMDF 库版本的驱动程序，然后后者必须更新。 有关更新的框架库的信息，请参阅[可再发行框架组件](installation-components-for-kmdf-drivers.md)。

（请注意 framework 共同的安装程序文件的名称，包括这两个主要和次要版本编号。 有关辅助安装程序文件的名称的详细信息，请参阅[使用 KMDF 共同安装程序](installing-the-framework-s-co-installer.md)。)

生成您的驱动程序时，MSBuild 实用工具将链接的包含 MSBuild 实用程序使用的库的版本号的存根 （stub） 文件的驱动程序。 当操作系统加载您的驱动程序时，框架的加载程序将检查驱动程序的存根 （stub） 以确定如果驱动程序将运行与系统上的框架库的版本中的版本信息。

若要确定您的驱动程序正在使用的库版本，该驱动程序可以调用[ **WdfDriverIsVersionAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverisversionavailable)或[ **WdfDriverRetrieveVersionString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverretrieveversionstring).

KMDF 库的发行历史记录的信息，请参阅[KMDF 版本历史记录](kmdf-version-history.md)。

## <a name="umdf"></a>UMDF


对于 KMDF，如 UMDF 库的主版本号会使用两个字符。 但是，主版本号仅显示在开头 UMDF 2.0 版的 UMDF 库文件名称。

UMDF 版本 2.0 中，UMDF 库的文件名称是*Wudfx02000.dll*。

对于 UMDF 版本 1。*x*，UMDF 库文件名称是*Wudfx.dll*。

KMDF 库的发行历史记录的信息，请参阅[UMDF 版本历史记录](umdf-version-history.md)。


 





