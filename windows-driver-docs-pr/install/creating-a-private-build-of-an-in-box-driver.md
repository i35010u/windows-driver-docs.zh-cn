---
title: 创建收件箱驱动程序的专用生成
description: 创建收件箱驱动程序的专用生成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f92523c0286d72abe4c5261d983c73a890209127
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827811"
---
# <a name="creating-a-private-build-of-an-inbox-driver"></a>创建收件箱驱动程序的专用生成


当你生成收件箱驱动程序的专用版并 [将 Windows 配置为平等地对驱动程序签名进行排序](configuring-windows-to-rank-driver-signatures-equally.md)时，你必须确保专用生成先 Microsoft 签名版本。 确保这一点的最简单方法是在 [驱动程序包的](driver-packages.md)inf 文件中更新 [**inf DriverVer 指令**](inf-driverver-directive.md)的值。 新值必须指定晚于目标系统上安装的包 INF 文件中的 **DriverVer** 指令值的日期和版本。

可以通过执行以下步骤，自动构建专用版收件箱驱动程序的过程：

1. 修改生成文件，为 [驱动程序包](driver-packages.md)生成新的 INF 文件。 例如，将以下行添加到 *生成文件*：

   ```cpp
   $(O)\sample.inf
   ```

2. 将指令添加到生成新 INF 文件的 *生成* 文件中，并执行 [STAMPINF](../devtest/stampinf.md) 工具对 INF 文件进行时间戳。 例如，下面的代码示例演示了如何创建名为 *Sample* 的 inf 文件并为其创建时间戳：

   ```cpp
   $(O)\ sample.inf: $(_INX)\ sample.inx $(_LNG)\ sample.txt
       $(C_PREPROCESSOR_NAME) $(PREFLAGS) $(_LNG)\$(@B).txt > $(O)\$(@B).txt1
       copy /b $(_INX)\$(@B).inx+$(O)\$(@B).txt1 $@
       @del $(O)\$(@B).txt1
       stampinf -f sample.inf -d * -v * -c MyCatalogFile.cat
       $(TSBINPLACE_CMD)
   ```

   在此示例中使用以下 [Stampinf](../devtest/stampinf.md) 命令行参数：

   - -D \* 参数使用当前日期作为 INF 文件中的 DriverVer 指令的一部分。
   - **-V \\** _ 参数对版本号使用当前时间。 如果已设置 STAMPINF_VERSION 环境变量，则 Stampinf 将使用此环境变量指定的版本号值。
   - -_ *C** 参数指定 [驱动程序包](driver-packages.md)的 [编录文件](catalog-files.md)的名称。 此值将写入生成的 IF 文件的 [**INF 版本部分**](inf-version-section.md)的 **CatalogFile** 指令。

   **注意**  如果 PRIVATE_DRIVER_PACKAGE 设置环境变量，则 Stampinf 将使用 INF **DriverVer** 指令的当前日期和版本。 通过设置此环境变量，无需在 *生成文件* 中使用 **-d** 或 **-v** 参数。

     

构建驱动程序后，您必须对 [驱动程序包](driver-packages.md)进行签名，并且必须使用 *生成文件* 中 [Stampinf](../devtest/stampinf.md)的 **-c** 参数中指定的同一 [目录文件](catalog-files.md)。 若要对驱动程序包进行签名，请按照在 [开发和测试过程中为驱动程序签名](./introduction-to-test-signing.md)中所述的步骤进行操作。

 

