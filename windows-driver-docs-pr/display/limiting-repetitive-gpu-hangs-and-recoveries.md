---
title: 限制重复 GPU 挂起和恢复
description: 限制重复 GPU 挂起和恢复
ms.assetid: e8ad0add-ecb2-4982-82bc-50f5ffbe4b0f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c50be80c19c4424d1538e3afdc05b31bdd49010
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526077"
---
# <a name="limiting-repetitive-gpu-hangs-and-recoveries"></a>限制重复 GPU 挂起和恢复


从 Windows Vista Service Pack 1 (SP1) 和 Windows Server 2008 开始，用户体验改进了在其中 GPU 挂起经常和快速的情况下。 重复 GPU 挂起指示没有已成功恢复图形硬件。 在这些情况下，最终用户必须关闭并重新启动操作系统完全重置图形硬件。 如果操作系统检测到六个或多个 GPU 挂起和后续恢复发生在 1 分钟内，操作系统 bug 检查下一步的 GPU 挂起的计算机。

 

 





