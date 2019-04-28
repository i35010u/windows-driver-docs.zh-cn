---
title: 重新处理库
description: 重新处理库
ms.assetid: 8d9f5890-cbe1-4240-ab23-76b6008fe686
keywords:
- 库 WDK Static Driver Verifier 重新处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c0734adc5d59005acb19dce9a2c2d7a3cbb6f9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340270"
---
# <a name="reprocessing-a-library"></a>重新处理库


通常需要处理的库的驱动程序需要一次的代码。 但是，您需要处理在以下情况下的库：

-   **添加的库**。 如果驱动程序代码中的更改需要 SDV 尚未处理的库，必须处理的库。

-   **库更改**。 如果代码的更改在驱动程序需要，库中或在库中所需的其中一个库，则必须重新处理受此更改影响的所有库。

-   **删除已处理的库**。 如果您的所有库从缓存中都删除库，通过使用**删除库**按钮**库**选项卡上或通过运行 **/clean**选项在 MSBuild 中的库目录。

如果出于任何原因，无法处理所需的库，你仍然可以运行验证，但结果是不太可靠。

**若要重新处理库**

1.  启动的 Static Driver Verifier。 从**驱动程序**Visual Studio 菜单中的单击**启动 Static Driver Verifier...**.
2.  上**Main**选项卡上，单击**清理**。
3.  单击**库**选项卡，单击**添加库**添加库。
4.  导航到的库目录，然后选择库的项目文件。

**若要重新处理所有的库**

1.  启动的 Static Driver Verifier。 从**驱动程序**Visual Studio 菜单中的单击**启动 Static Driver Verifier...**.
2.  单击**库**选项卡以选择库 （或库），然后单击**删除库**若要从缓存中删除的库。
3.  对于需要重新处理每个库，请单击**添加库**。
4.  导航到的库目录，然后选择库的项目文件。
5.  重复步骤以添加并选择您的驱动程序使用每个库的项目文件。

您还可以重新从库中的 MSBuild 命令处理通过使用 /clean 和 /lib 参数选项。 有关详细信息，请参阅[Static Driver Verifier 命令 (MSBuild)](-static-driver-verifier-commands--msbuild-.md)。

 

 





