---
title: 目录文件和数字签名
description: 目录文件和数字签名
ms.assetid: e5504823-1c7e-4cbf-9d42-49e09aeae9d4
keywords:
- 指纹 WDK 驱动程序签名
- 签名的编录文件 WDK 驱动程序签名
- .cat 文件
- CAT 文件
- 驱动程序签名 WDK，目录文件
- 签名的驱动程序 WDK，目录文件
- 数字签名 WDK，目录文件
- 签名 WDK，目录文件
- 目录文件 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e07cc4b25d4f4603bc7832fe75a65c571ecd036a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520708"
---
# <a name="catalog-files-and-digital-signatures"></a>目录文件和数字签名


数字签名的编录文件 (*.cat*) 可以用作的文件的任意集合的数字签名。 目录文件包含一系列加密哈希，或*指纹*。 每个指纹对应于在集合中包含一个文件。

插即用 (PnP) 设备安装可识别的签名的编录文件[驱动程序包](driver-packages.md)作为[数字签名](digital-signatures.md)驱动程序包，其中目录文件中的每个指纹对应于驱动程序包的安装文件。 无论使用什么目标操作系统，使用加密技术对数字签名的编录文件。

即插即用设备安装会考虑的数字签名[驱动程序包](driver-packages.md)如果驱动程序包进行签名之后更改的驱动程序包中的任何文件无效。 此类文件包括 INF 文件、 目录文件，并通过复制的所有文件[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)。 例如，甚至单字节更改来更正拼写错误使数字签名无效。 如果数字签名无效，必须可以重新提交到驱动程序包[Windows 硬件质量实验室 (WHQL)](https://go.microsoft.com/fwlink/p/?linkid=8705)的新签名或生成一个新[Authenticode](authenticode.md)签名的驱动程序包。

同样，对设备的硬件或固件的更改要求修订后[设备 ID](device-ids.md)值，以便系统可以检测到更新的设备并安装正确的驱动程序。 修改后的设备 ID 值必须出现在 INF 文件，因为必须重新提交到 WHQL 为一个新的签名的包或生成一个新[Authenticode](authenticode.md)驱动程序包的签名。 即使不会更改驱动程序二进制文件时，必须执行此操作。

**CatalogFile**指令[ **INF 版本部分**](inf-version-section.md)的驱动程序[INF 文件](overview-of-inf-files.md)指定的目录文件的名称驱动程序包。 在驱动程序安装过程中使用的操作系统**CatalogFile**指令以识别并验证目录文件。 系统会复制到的目录文件 *%systemroot%\\CatRoot*目录，然后 INF 文件到 *%systemroot%\\Inf*目录。

### <a name="guidelines-for-catalog-files"></a>目录文件的准则

从 Windows 2000 开始，如果[驱动程序包](driver-packages.md)安装在所有版本的 Windows，INF 文件相同的二进制文件可以包含单一的未修饰**CatalogFile**指令。 但是，如果包安装不同的二进制文件的不同版本的 Windows，INF 文件应包含修饰**CatalogFile**指令。 有关详细信息**CatalogFile**指令，请参阅[ **INF 版本部分**](inf-version-section.md)。

如果有多个驱动程序包时，应创建每个驱动程序包的单独目录文件，并为每个目录文件提供一个唯一的文件名称。 两个不相关的驱动程序包不能共享一个目录文件。 但是，单个驱动程序包，具有多个设备需要只有一个目录文件。

 

 





