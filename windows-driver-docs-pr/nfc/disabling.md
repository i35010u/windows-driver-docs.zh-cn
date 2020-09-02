---
title: 禁用 NFP
description: 客户端可以暂时禁用订阅、发布和状态显示。
ms.assetid: 94BE6D24-60AD-45BD-AF2D-388022114975
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 045be0930a196bf15082cdbb29520a9837ea9a2c
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382827"
---
# <a name="disabling-nfp"></a>禁用 NFP


客户端可以暂时禁用订阅、发布和状态显示。

通过向句柄发送 [**IOCTL \_ NFP \_ DISABLE**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable) 来暂时禁用订阅、发布和状态显示。 当客户端想要禁用邻近功能但保留分配的资源以在需要时快速重新启用它们时，这非常有用。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)