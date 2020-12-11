---
title: 禁用 NFP
description: 客户端可以暂时禁用订阅、发布和状态显示。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60c90c9b8601714500fc74cd4c049480f59c95a9
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091022"
---
# <a name="disabling-nfp"></a>禁用 NFP


客户端可以暂时禁用订阅、发布和状态显示。

通过向句柄发送 [**IOCTL \_ NFP \_ DISABLE**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable) 来暂时禁用订阅、发布和状态显示。 当客户端想要禁用邻近功能但保留分配的资源以在需要时快速重新启用它们时，这非常有用。

 

 
## <a name="related-topics"></a>相关主题
[近现场通信 (NFC) API 参考](/windows-hardware/drivers/ddi/_nfpdrivers/)
