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
ms.openlocfilehash: 130d280898b4c76193e6698ba69d92c2156b5016
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813596"
---
# <a name="disabling-nfp"></a>禁用 NFP


客户端可以暂时禁用订阅、发布和状态显示。

通过向句柄发送 [**IOCTL \_ NFP \_ DISABLE**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable) 来暂时禁用订阅、发布和状态显示。 当客户端想要禁用邻近功能但保留分配的资源以在需要时快速重新启用它们时，这非常有用。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)
