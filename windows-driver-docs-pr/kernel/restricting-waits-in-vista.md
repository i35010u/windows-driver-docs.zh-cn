---
title: 在 Vista 中限制等待
description: 在 Vista 中限制等待
ms.assetid: edcc25d0-bcf6-48f0-832e-3f911bd42142
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c85817e95bfe65093f1ad221bcdb531f8f4f630c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521753"
---
# <a name="restricting-waits-in-vista"></a>在 Vista 中限制等待


因为多个设备驱动程序开发人员使用[同步 I/O 编程技术](synchronous-i-o-programming.md)，Windows 可以慢，或者"冻结"时在设备的响应时间。 若要减少此问题，Vista 中的 I/O 管理器将停止执行"进入"正在等待设备在一段时间后响应的程序。

**请注意**  强烈建议[同步 I/O 编程技术](synchronous-i-o-programming.md)避免设备驱动程序中。 如果 Vista 停止驱动程序代码的执行，因为您的驱动程序正在等待设备，你的设备可能会处于未知状态。

 

 

 




