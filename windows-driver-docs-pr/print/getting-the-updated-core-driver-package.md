---
title: 获取更新的核心驱动程序包
description: 获取更新的核心驱动程序包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec7ee0b5f3202018d22db7c80b41cc743de3d49c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835865"
---
# <a name="getting-the-updated-core-driver-package"></a>获取更新的核心驱动程序包

[获取](constructing-a-package-aware-driver-with-updated-core-drivers.md)Microsoft 独立更新 (MSU) 文件包含更新后的核心驱动程序包后，下一步是扩展 MSU 文件的内容。

若要使该核心驱动程序包的内容可供 PnP 安装程序访问，请打开命令提示符窗口，并使用 expand 命令展开 MSU 文件。 还将适当的 cabinet ( .cab) 文件中，该文件的名称以 "Windows 6.0-" 开头，此名称包含在 MSU 文件中。

下面的示例演示如何使用 [**expand**](/previous-versions/windows/it-pro/windows-xp/bb490903(v=technet.10)) 命令，该命令应在包含 MSU 文件的目录中执行：

```cpp
expand Windows6.0-KB123456-x86.MSU [dest directory] -F:*
expand Windows6.0-KB123456-x86.CAB [dest directory] -F:*
```

在这两个命令之后，目录将包含多个清单文件和子目录。 其中一个子目录将包含 Ntprint.inf 和未压缩的驱动程序组件。 此目录的名称以修补程序的处理器体系结构开头 (例如，x86) ，附加到的 "ntprint.inf"、GUID 和其他跟踪信息。
