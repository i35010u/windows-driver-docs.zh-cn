---
title: 更新非包感知驱动程序的核心驱动程序文件
description: 更新非包感知驱动程序的核心驱动程序文件
ms.assetid: ce5da376-edac-4cd1-8750-9981bb5b709d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f174f0fb17e62ba247650ad611349bd226ebb89
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734415"
---
# <a name="updating-core-drivers-files-for-non-package-aware-drivers"></a>更新非包感知驱动程序的核心驱动程序文件

Windows Vista 之前的 Windows 操作系统（包括 Windows Server 2003、Windows XP 和 Windows 2000）的核心驱动程序组件在 Microsoft [Connect](/collaborate/connect-redirect) 网站上作为 XPSDrv、UniDrv 和 PostScript 驱动程序的单独包提供。 每个包都有不同的再发行协议。 实际上，包中的文件与 Windows Vista 中的对应文件完全相同。 若要解压缩驱动程序文件，请按照 [获取更新核心驱动程序包](getting-the-updated-core-driver-package.md)中列出的步骤进行操作。 扩展核心驱动程序包后，请将所需的核心驱动程序文件包含在自己的驱动程序包中，就像它们是驱动程序的一部分一样。 换句话说，将驱动程序二进制文件从核心包复制到驱动程序包的主目录。 这将破坏数字签名核心驱动程序包的完整性，但它会使 Windows XP (和 windows Vista 之前的其他 Windows 操作系统) 和不能识别包的驱动程序利用核心驱动程序更新。

请注意，未更改的核心驱动程序包仍可存储在驱动程序包的单独子目录中，以在 Windows Vista 中启用包感知安装。 也就是说，你可以为 Windows Vista 和 Windows XP 发布一个驱动程序包。 包中的 INF 文件应基于安装包的操作系统为核心驱动程序文件选择相应的源。 对于 Windows Vista，INF 文件应从驱动程序包中的子目录安装未修改的核心驱动程序包。 对于 Windows XP，INF 文件应安装包的主目录中的可再发行核心驱动程序文件。

对于 Windows Vista，应避免分解核心驱动程序包，也不要将核心驱动程序文件直接作为驱动程序包的一部分进行引用。 否则，包可能看起来可以在 Windows Vista 中正确安装，但结果可能是打印系统不稳定和功能退化。 若要避免此类问题，请广泛测试驱动程序更新包，验证它是否在 Windows Vista 和 Windows XP 上正确安装。

有关详细信息，请参阅 [创建适用于 WINDOWS XP 和 Windows Vista 的单个驱动程序包](creating-a-single-driver-package-for-windows-xp-and-windows-vista.md)。