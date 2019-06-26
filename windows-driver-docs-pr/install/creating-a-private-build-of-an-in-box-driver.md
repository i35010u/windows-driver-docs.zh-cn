---
title: 创建收件箱驱动程序对专用生成
description: 创建收件箱驱动程序对专用生成
ms.assetid: aed3c175-3e95-4bfb-a514-a663dd9e3f57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 953d8cdb3de7f61ad2ee3dab648ccc0c0258a1bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356315"
---
# <a name="creating-a-private-build-of-an-inbox-driver"></a>创建收件箱驱动程序对专用生成


当生成私有版本的收件箱驱动程序，并[Windows 同样配置为排名驱动程序签名](configuring-windows-to-rank-driver-signatures-equally.md)，必须确保专用生成优先于 Microsoft 签名版本。 若要确保这一点的最简单方法是更新的值[ **INF DriverVer 指令**](inf-driverver-directive.md)中[驱动程序包的](driver-packages.md)INF 文件。 新值必须指定日期和版本的值低于**DriverVer**指令目标系统安装的包的 INF 文件中。

可以自动完成构建私有版本的优先 Microsoft 签名版本于通过执行以下步骤的收件箱驱动程序的过程：

1. 修改生成文件生成新的 INF 文件[驱动程序包](driver-packages.md)。 例如，添加下面的代码行*生成文件*:

   ```cpp
   $(O)\sample.inf
   ```

2. 添加到的指令*生成文件*，将生成新的 INF 文件并执行[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)工具到时间戳的 INF 文件。 例如，下面的代码示例显示了如何可以创建和时间戳的 INF 文件，名为*Sample.inf*:

   ```cpp
   $(O)\ sample.inf: $(_INX)\ sample.inx $(_LNG)\ sample.txt
       $(C_PREPROCESSOR_NAME) $(PREFLAGS) $(_LNG)\$(@B).txt > $(O)\$(@B).txt1
       copy /b $(_INX)\$(@B).inx+$(O)\$(@B).txt1 $@
       @del $(O)\$(@B).txt1
       stampinf -f sample.inf -d * -v * -c MyCatalogFile.cat
       $(TSBINPLACE_CMD)
   ```

   以下[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)在此示例中使用命令行参数：

   - -D\*参数使用当前日期作为 INF 文件中的 DriverVer 指令的一部分。
   - **-V \\** * 参数的版本号为使用当前时间。 如果已设置 STAMPINF_VERSION 环境变量，则 Stampinf 将使用此环境变量指定的版本号值。
   - -**C**参数指定的名称[编录文件](catalog-files.md)有关[驱动程序包](driver-packages.md)。 此值写入**CatalogFile**指令[ **INF 版本部分**](inf-version-section.md)生成如果文件。

   **请注意**Stampinf 为 INF 中设置环境变量 PRIVATE_DRIVER_PACKAGE，如果使用的当前日期和版本**DriverVer**指令。 通过设置此环境变量，您不必使用 **-d**或 **-v**中的参数你*生成文件*。

     

该驱动程序构建后，您必须签署[驱动程序包](driver-packages.md)，并且必须使用相同[编录文件](catalog-files.md)中指定 **-c**参数[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)内你*生成文件*。 若要签署驱动程序包，请按照中所述的步骤[签名的驱动程序在开发和测试](signing-drivers-during-development-and-test.md)。

 

 





