---
title: 获取更新的核心驱动程序包
description: 获取更新的核心驱动程序包
ms.assetid: 7fac00e4-1d3e-4bb7-95cd-298176de374d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f92bf4d0523217ed0d4fe47fbeb45fcb28e88a28
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210905"
---
# <a name="getting-the-updated-core-driver-package"></a>获取更新的核心驱动程序包

[获取](constructing-a-package-aware-driver-with-updated-core-drivers.md)包含更新核心驱动程序包的 Microsoft 独立更新（MSU）文件后，下一步是扩展 MSU 文件的内容。

若要使该核心驱动程序包的内容可供 PnP 安装程序访问，请打开命令提示符窗口，并使用 expand 命令展开 MSU 文件。 还展开相应的 cabinet （.cab）文件（该文件的名称以 "Windows 6.0-" 开头），该文件包含在 MSU 文件中。

下面的示例演示如何使用[**expand**](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-xp/bb490903(v=technet.10))命令，该命令应在包含 MSU 文件的目录中执行：

```cpp
expand Windows6.0-KB123456-x86.MSU [dest directory] -F:*
expand Windows6.0-KB123456-x86.CAB [dest directory] -F:*
```

在这两个命令之后，目录将包含多个清单文件和子目录。 其中一个子目录将包含 Ntprint.inf 和未压缩的驱动程序组件。 此目录的名称以修补程序的处理器体系结构（例如 x86）开头，附加到的是 "ntprint.inf"、GUID 和其他跟踪信息。
