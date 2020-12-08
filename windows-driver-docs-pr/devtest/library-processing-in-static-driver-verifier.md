---
title: 静态驱动程序验证程序中的库处理
description: 静态驱动程序验证程序中的库处理
keywords:
- 静态驱动程序验证程序 WDK，库
- StaticDV WDK，库
- SDV WDK，库
- 库 WDK 静态驱动程序验证程序
- 库 WDK 静态驱动程序验证程序，关于库处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2d47e24818c87aee0bdb2583f4438f41247106d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833533"
---
# <a name="library-processing-in-static-driver-verifier"></a>静态驱动程序验证程序中的库处理


许多驱动程序依赖于动态和静态链接的函数库。 通常，这些库包括常规处理函数，但在某些情况下，它们包括驱动程序的一部分功能。

库对于确定驱动程序是否符合界面规则非常重要。 例如，如果不使用库代码，驱动程序可能看不到库中包含的所需调用。 或者，该库可能包含驱动程序重复的调用，导致重复错误，如释放锁定两次。

若要在验证驱动程序时包含库，SDV 必须首先 [处理库](processing-a-library.md) ，以便准备用于验证驱动程序。

SDV 会尝试自动检测并处理驱动程序所依赖的所有库，但由于它不知道某些库源文件的位置，因此它无法自动处理这些库，并将它们包含在驱动程序验证中。 若要确保 SDV 提供最准确的驱动程序分析，应通过单击 " **库** " 选项卡并选择 " **添加库** " 来处理库，手动将驱动程序引用添加到 SDV 的库缓存。  如果在命令行中运行，则可以通过对库项目运行包含 **/lib** 命令的 sdv 来添加库。

SDV 处理库后，它会保留该库的处理文件，并自动在验证所有需要库的驱动程序时包括库代码。 如果库代码发生更改，则无需重新处理库。 有关重新处理库的说明，请参阅重新处理 [库](reprocessing-a-library.md)。

本节包括：

[处理库](processing-a-library.md)

[重新处理库](reprocessing-a-library.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

SDV 包括系统库的已处理库文件。 不需要直接 SDV 来处理这些库。 当 SDV 检测到驱动程序依赖于这些库时，将为这些库使用其处理的文件，而不显示警告消息。 有关库要求的信息，请参阅 [确定 Static Driver Verifier 是否支持驱动程序或库](determining-if-static-driver-verifier-supports-your-driver-or-library.md)。

 

 





