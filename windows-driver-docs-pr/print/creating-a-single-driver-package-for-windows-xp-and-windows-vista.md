---
title: 创建适用于 Windows XP 和 Windows Vista 的单个驱动程序包
description: 创建适用于 Windows XP 和 Windows Vista 的单个驱动程序包
ms.assetid: 5e350152-edd7-4afb-bcba-dd0217d0d17a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9509c95833777b04d7ca09be994f307169c81ce7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372430"
---
# <a name="creating-a-single-driver-package-for-windows-xp-and-windows-vista"></a>创建适用于 Windows XP 和 Windows Vista 的单个驱动程序包


在 Microsoft [Connect](https://go.microsoft.com/fwlink/p/?linkid=133880)网站提供了两个核心驱动程序更新的组：

-   早于 Windows Vista （包括 Windows Server 2003、 Windows XP 和 Windows 2000），对于 Windows 操作系统的一组可再发行组件更新允许硬件制造商将合并所需支持这些操作系统的特定文件.

-   适用于 Windows Vista 及更高版本，一个单独的包允许硬件制造商提供的最新的核心驱动程序包。

若要同时支持 Windows XP （和其他 Windows 操作系统早于 Windows Vista） 和 Windows Vista 和更高版本操作系统中相同的驱动程序包，硬件制造商必须使用相应的可再发行组件包，并构造其 INF相应地。

### <a name="no-redistributable-package"></a>没有可再发行组件包

如果您的驱动程序与 Windows XP 和 Windows Vista 版本的核心驱动程序组件 （即，如果不重新分发的核心驱动程序是必需的） 工作原理，请执行以下步骤：

1.  继续在 Windows Vista 上使用 Windows XP 驱动程序。 不不需要任何更改。

2.  对于 Windows Vista Premium 徽标认证，Windows XP （以及其他 Windows 操作系统早于 Windows Vista） 提供单独的 INF 安装部分和 Windows Vista 的 Windows Vista 和更高版本的操作系统，以及使 INF 安装部分识别的包。

### <a href="" id="redistributable-package-for-windows-operating-systems-earlier-than-win"></a> 可再发行组件包适用于 Windows 操作系统早于 Windows Vista

如果您的驱动程序适用于初始的 Windows Vista 版本，但需要在 Windows XP 和早期版本的操作系统上工作的核心驱动程序组件的 Windows Vista 版本 (即，如果早于 Windows Vista 重新分发的 Windows 操作系统是必需的），请执行以下步骤：

1.  创建单独的 INF 安装部分适用于 Windows XP （和其他 Windows 操作系统早于 Windows Vista） 和适用于 Windows Vista （和更高版本）。

2.  使用 INF **CoreDriverDependencies**并**CoreDriverSections**指令来强制使用收件箱核心驱动程序包的 INF 文件的 Windows Vista 部分。

3.  确定从重新分发包的 Windows 操作系统早于 Windows Vista，支持这些操作系统版本所需的文件。

4.  对于下层支持必需的二进制文件包含在驱动程序软件包，并仅将它们复制为早于 Windows Vista 安装在 Windows 操作系统上。

### <a name="windows-vista-redistributable-package"></a>Windows Vista 可再发行组件包

如果您的驱动程序需要更新版本的核心驱动程序包，若要正常运行和 Windows XP 上的初始 Windows Vista 版本 （即，如果需要进行重新分发到 Windows Vista），请执行以下步骤：

1.  创建单独的 INF 安装部分适用于 Windows XP （和其他 Windows 操作系统早于 Windows Vista） 和适用于 Windows Vista 及更高版本。

2.  驱动程序包的子目录中包括整个 Windows Vista 核心驱动程序包。

3.  使用[ **INF CopyINF 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyinf-directive)预更新的核心驱动程序加载到驱动程序存储区。

4.  使用 INF **InboxVersionRequired**= *&lt;更新的核心驱动程序版本&gt;* 指令以确保只有较新版本的核心驱动程序包使用。

5.  使用 INF **CoreDriverDependencies**并**CoreDriverSections**指令指示您的 Windows Vista 驱动程序需要更新的核心驱动程序。

6.  在 Windows 操作系统早于 Windows Vista 在安装部分中，复制所需的文件直接从包含的核心驱动程序包，就像您的驱动程序的一部分。

 

 




