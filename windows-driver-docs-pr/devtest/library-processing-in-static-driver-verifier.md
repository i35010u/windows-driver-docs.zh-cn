---
title: 静态驱动程序验证程序中的库处理
description: 静态驱动程序验证程序中的库处理
ms.assetid: d95ccdc2-aa00-4671-87fb-6f0f77d2ba8d
keywords:
- 静态驱动程序验证程序 WDK 库
- StaticDV WDK 库
- SDV WDK 库
- 库 WDK Static Driver Verifier
- 有关库处理库 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 477b8fdf07195cebd7f1f6927c903d477f4943c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564168"
---
# <a name="library-processing-in-static-driver-verifier"></a>静态驱动程序验证程序中的库处理


许多驱动程序依赖于函数的动态和静态链接的库。 通常情况下，这些库包括常规处理函数，但在某些情况下，它们包括是不可缺少的驱动程序的功能。

库是必需的驱动程序是否符合接口规则确定的。 例如，而无需库代码中，驱动程序看起来已经遗漏了库中包含的所需的调用。 或者，该库可能会包含该驱动程序重复项，这会导致重复的错误，如两次释放锁的调用。

若要验证的驱动程序包含一个库，SDV 必须首先[处理库](processing-a-library.md)以准备用于验证该驱动程序。

SDV 尝试自动检测并处理该驱动程序所依赖的所有库，但它不知道某些库源文件的位置，因为它无法自动都处理这些库并将其包括在驱动程序验证。 若要确保 SDV 为您的驱动程序提供最准确的分析，则应手动添加任何库对 SDV 的库缓存在驱动程序的引用通过单击**库**选项卡并选择**添加库**来处理库。  如果运行命令行中，可能会将库添加通过运行使用的 sdv **/lib**命令对类库项目。

SDV 处理库后，它将保留该库及其处理文件，并会自动验证所有驱动程序的需要在库中包括的库代码。 不需要重新处理库，除非库代码发生更改。 有关重新处理库的说明，请参阅[重新处理一个库](reprocessing-a-library.md)。

本部分包括：

[正在处理库](processing-a-library.md)

[重新处理库](reprocessing-a-library.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

SDV 包括系统库的已处理的库文件。 不需要直接 SDV 来处理这些库。 当 SDV 检测到驱动程序依赖于这些库时，它为这些库已处理的文件而不会显示一条警告消息使用。 有关库要求的信息，请参阅[确定驱动程序或库是否支持 Static Driver Verifier](determining-if-static-driver-verifier-supports-your-driver-or-library.md)。

 

 





