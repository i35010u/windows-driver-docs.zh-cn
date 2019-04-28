---
title: 安全测试
description: 安全测试
ms.assetid: d9d98f18-a7fc-479c-8627-0aea53ff0bae
keywords:
- 安全 WDK 文件系统、 测试
- 测试安全 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789135085fac63ddb56c9a9285f42cd352d903fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344357"
---
# <a name="testing-for-security"></a>安全测试


## <span id="ddk_testing_for_security_if"></span><span id="DDK_TESTING_FOR_SECURITY_IF"></span>


测试安全不是一个自动化的过程。 相反，它将结合使用现有工具，以及在给定的驱动程序或驱动程序的全面的威胁分析。 测试驱动程序因此包含许多单独的步骤：

-   全面的威胁分析以主动找出的可能在其中使用该驱动程序的环境中进行的攻击类型。 例如，在高度受控环境中存在的驱动程序可能比大容量分发，这将遵循任意攻击的驱动程序的更简单威胁分析。

-   使用 WDK 设备路径试验程序，例如中包括"设计 Windows"徽标测试的现有工具测试设备来控制测试实用程序的攻击。 此外应使用 IFS 测试在 WDK 中的彻底测试存储堆栈问题。

-   测试标识为威胁分析的一部分的方案中特别是正常的驱动程序开发的一部分，应开发其他测试。 这些测试通常会是唯一的驱动程序并尝试探测的特定驱动程序。

理想情况下，出于测试目的，验证测试的开发将包括来自的软件，以及不相关的开发资源与特定类型的文件系统或文件系统筛选器驱动程序产品所熟悉的原始设计器的输入开发，以及一个或多个人员熟悉安全入侵分析和防护。

 

 




