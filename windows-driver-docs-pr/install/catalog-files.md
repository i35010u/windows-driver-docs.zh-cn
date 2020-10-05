---
title: 目录文件和数字签名
description: 目录文件和数字签名
ms.assetid: e5504823-1c7e-4cbf-9d42-49e09aeae9d4
keywords:
- 指纹 WDK 驱动程序签名
- 签名目录文件 WDK 驱动程序签名
- .cat 文件
- CAT 文件
- 驱动程序签名 WDK，编录文件
- 对驱动程序进行签名 WDK，编录文件
- 数字签名 WDK，目录文件
- 签名 WDK，编录文件
- 目录文件 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f726f04e8003a7c4c655e64b73daa82c6832b627
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734271"
---
# <a name="catalog-files-and-digital-signatures"></a>目录文件和数字签名


已数字签名的目录文件 (*.cat*) 可用作任意文件集合的数字签名。 目录文件包含加密哈希或 *指纹*的集合。 每个指纹对应于集合中包含的一个文件。

即插即用 (PnP) 设备安装将 [驱动程序包](driver-packages.md) 的签名目录文件识别为驱动程序包的 [数字签名](digital-signatures.md) ，其中目录文件中的每个指纹与驱动程序包安装的文件相对应。 无论使用何种操作系统，都将使用加密技术对编录文件进行数字签名。

如果在对驱动程序包进行签名之后更改了驱动程序包中的任何文件，则 PnP 设备安装会认为该驱动 [程序包](driver-packages.md) 的数字签名无效。 此类文件包括 INF 文件、目录文件以及由 [**Inf CopyFiles 指令**](inf-copyfiles-directive.md)复制的所有文件。 例如，即使更正拼写错误的单字节更改也会使数字签名失效。 如果数字签名无效，则必须将驱动程序包重新提交给 [Windows 硬件质量实验室 (](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) 新签名的 WHQL) 或为驱动程序包生成新的 [Authenticode](authenticode.md) 签名。

同样，更改设备的硬件或固件需要修改的 [设备 ID](device-ids.md) 值，以便系统可以检测更新的设备并安装正确的驱动程序。 由于修改后的设备 ID 值必须出现在 INF 文件中，因此必须将包重新提交给 WHQL 以获取新签名，或为驱动程序包生成新的 [Authenticode](authenticode.md) 签名。 即使驱动程序二进制文件未更改，也必须执行此操作。

驱动程序的[inf 文件](overview-of-inf-files.md)的 " [**inf 版本" 部分**](inf-version-section.md)中的**CatalogFile**指令指定驱动程序包的编录文件的名称。 在驱动程序安装过程中，操作系统使用 **CatalogFile** 指令来识别和验证目录文件。 系统将目录文件复制到 *% systemroot% \\ CatRoot* 目录，将 INF 文件复制到 *% systemroot% \\ INF* 目录。

### <a name="guidelines-for-catalog-files"></a>目录文件指南

从 Windows 2000 开始，如果 [驱动程序包](driver-packages.md) 在所有版本的 Windows 上安装了相同的二进制文件，则 INF 文件可包含单个未修饰的 **CatalogFile** 指令。 但是，如果包为不同版本的 Windows 安装了不同的二进制文件，则 INF 文件应包含修饰的 **CatalogFile** 指令。 有关 **CatalogFile** 指令的详细信息，请参阅 [**INF 版本部分**](inf-version-section.md)。

如果有多个驱动程序包，则应该为每个驱动程序包创建一个单独的目录文件，并为每个目录文件指定一个唯一的文件名。 两个不相关的驱动程序包不能共享一个编录文件。 但是，为多个设备提供服务的单个驱动程序包只需要一个编录文件。

 

