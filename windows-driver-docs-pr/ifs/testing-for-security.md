---
title: 安全测试
description: 安全测试
keywords:
- 安全 WDK 文件系统，测试
- 测试安全 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfabc9b7e5f7aa49c96f51ce1475bf6b5419c346
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817339"
---
# <a name="testing-for-security"></a>安全测试


## <span id="ddk_testing_for_security_if"></span><span id="DDK_TESTING_FOR_SECURITY_IF"></span>


安全测试不是一种自动化的过程。 相反，它结合了现有工具的使用以及给定的驱动程序或驱动程序的全面威胁分析。 测试驱动程序的操作包括多个单独的步骤：

-   用于主动识别在使用驱动程序的环境中可能会发生的攻击类型的全面威胁分析。 例如，在高度控制的环境中存在的驱动程序的威胁分析比用于大容量分发的驱动程序更简单，这会受到任意攻击。

-   使用现有工具（包括在 WDK 中设计的适用于 Windows 的 "徽标测试"）进行测试，例如设备路径试验、设备控制攻击测试实用工具。 WDK 中的 IFS 测试还应用于全面测试存储堆栈问题。

-   应将其他测试作为常规驱动程序开发的一部分进行开发，以便专门测试确定为威胁分析一部分的方案。 这些测试通常对驱动程序是唯一的，并尝试探测特定驱动程序。

理想情况下，出于测试目的，验证测试的开发将包括来自该软件的原始设计器的输入，以及熟悉开发的特定类型的文件系统或文件系统筛选器驱动程序产品的无关开发资源，以及一个或多个熟悉安全入侵分析和防护的人。

 

 




