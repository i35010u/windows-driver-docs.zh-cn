---
title: 获取更新的核心驱动程序包
description: 获取更新的核心驱动程序包
ms.assetid: 7fac00e4-1d3e-4bb7-95cd-298176de374d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27a842159c15ef3cf86e39a8048854e0fd5137b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385212"
---
# <a name="getting-the-updated-core-driver-package"></a>获取更新的核心驱动程序包


检查完[获取](constructing-a-package-aware-driver-with-updated-core-drivers.md)Microsoft 独立更新 (MSU) 文件包含更新的核心驱动程序包下, 一步是展开 MSU 文件的内容。

若要使核心驱动程序包的内容访问的即插即用安装程序，打开命令提示符窗口，并使用展开命令扩展 MSU 文件。 此外可以展开相应 cab (.cab) 文件，该名称以"Windows6.0-"，在 MSU 文件中包含的文件。

下面的示例演示如何使用**展开**命令，应在包含 MSU 文件的目录中执行该命令：

```cpp
expand Windows6.0-KB123456-x86.MSU [dest directory] -F:*
expand Windows6.0-KB123456-x86.CAB [dest directory] -F:*
```

以下这两个命令中，目录将包含大量的清单文件和子目录。 这些子目录中的一个将包含 Ntprint.inf 和未压缩的驱动程序组件。 此目录已向其追加"ntprint.inf"、 GUID 和其他跟踪信息以开头的修补程序 (例如，x86) 的处理器体系结构的名称。 有关详细信息，请参阅的定义**展开**命令在 Microsoft [TechNet](https://go.microsoft.com/fwlink/p/?linkid=122164) Web 站点。

 

 




