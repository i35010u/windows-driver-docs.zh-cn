---
title: 不识别包的驱动程序更新核心驱动程序文件
description: 不识别包的驱动程序更新核心驱动程序文件
ms.assetid: ce5da376-edac-4cd1-8750-9981bb5b709d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c4e01fbef1146d184f1d1f9f114a93486862ff2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525889"
---
# <a name="updating-core-drivers-files-for-non-package-aware-drivers"></a>不识别包的驱动程序更新核心驱动程序文件


核心驱动程序 Windows 早操作系统比 Windows Vista，包括 Windows Server 2003、 Windows XP 和 Windows 2000 中，提供了用于组件在 Microsoft [Connect](https://go.microsoft.com/fwlink/p/?linkid=133880) XPSDrv，不同的软件包的网站UniDrv 和 PostScript 驱动程序。 每个包具有不同的再分发协议。 包中的文件，实际上是，与 Windows Vista 中的对应项相同。 若要解压缩驱动程序文件，请按照中列出的步骤[获取更新核心驱动程序包](getting-the-updated-core-driver-package.md)。 一旦具有展开核心驱动程序包，包含就像您的驱动程序的一部分，您需要自己的驱动程序包中的核心驱动程序文件。 换而言之，将驱动程序二进制文件从核心包复制到驱动程序包的主目录。 这将中断的包的完整性进行数字签名的核心驱动程序，但它可实现 Windows XP （和其他 Windows 操作系统早于 Windows Vista） 和驱动程序不打包注意若要利用核心驱动程序更新。

请注意，未更改的核心驱动程序包可以仍存储在驱动程序包，以使 Windows Vista 中识别包的安装中的单独子目录中。 也就是说，你可以为 Windows Vista 和 Windows XP 释放一个驱动程序包。 在包中的 INF 文件应该选择相应的源以在其安装包的操作系统上基于的核心驱动程序文件。 对于 Windows Vista，INF 文件都应安装未更改的核心驱动程序包从驱动程序包中的子目录。 为 Windows XP 的 INF 文件应从包的主目录安装可再发行组件的核心驱动程序文件。

Windows Vista 中，应避免分解核心驱动程序包而不引用直接作为驱动程序包的一部分的核心驱动程序文件。 否则为包可能看起来正确安装在 Windows Vista 中，但结果可能是打印系统不稳定和回归的功能。 若要避免此类问题，测试驱动程序更新包广泛，若要验证其在 Windows Vista 和 Windows XP 上正确安装。

有关详细信息，请参阅[创建一个驱动程序程序包适用于 Windows XP 和 Windows Vista](creating-a-single-driver-package-for-windows-xp-and-windows-vista.md)。

 

 




