---
title: UMDF 设置（仅供测试）选项卡
description: 本主题详细介绍 WDF 验证程序 （测试使用仅限） UMDF 设置页。
ms.assetid: cce75c2e-fc93-4c17-9560-aef55451528b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acf49611495268e7c09928fe521b4c05b5c3378b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566021"
---
# <a name="umdf-settings-test-use-only-tab"></a>UMDF 设置（仅供测试）选项卡


本主题详细介绍了 WDF Verifier **UMDF 设置 （测试使用仅限）** 页。 在此页上，您可以更改可帮助测试一个或多个用户模式驱动程序框架 (UMDF) 驱动程序的整体系统的设置。

出于测试目的使用这些设置。 完成后测试中，单击**还原为默认值**按钮。 否则，您的计算机可能会出现显著的性能降低。

![方 umdf 设置 （仅供测试使用） 选项卡的屏幕截图](images/wdfverifier-tab4.png)

默认情况下[UMDF 正在进行记录器 (IFR)](https://msdn.microsoft.com/library/windows/hardware/ff545531)以便日志可以保留系统崩溃时存储在非分页内存中。 但是，在极少数情况下，可能需要在非分页内存中释放空间。 例如，可能是测试包含多个 UMDF 驱动程序的系统的压力[设备池](https://msdn.microsoft.com/library/windows/hardware/hh463993)是关闭，和非分页内存超出。 可以通过选择来获取可用的非分页内存略微提高**使用分页缓冲池**框。

此外，有时分析等工具驱动程序验证程序可能会降低系统性能足够的 CPU 密集型测试默认 UMDF 超时触发即使驱动程序未进行任何处理错误。 在这种情况下，增加超时值可能会降低这种类型的意外超时。

**警告**  
使用这些选项实际上可减少诊断 UMDF 驱动程序失败，因此你应使用它们仅在需要时或捕获的可能性。 它们是更有可能是用于测试整个系统。

 

 

 





