---
title: 禁用 NFP
description: 客户端可以暂时禁用订阅、发布和状态显示。
ms.assetid: 94BE6D24-60AD-45BD-AF2D-388022114975
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1c8f5850637cd8fc78f1735e67795a3c56aa0f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843423"
---
# <a name="disabling-nfp"></a>禁用 NFP


客户端可以暂时禁用订阅、发布和状态显示。

通过将[**IOCTL\_NFP\_DISABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable)发送到句柄来暂时禁用订阅、发布和状态。 当客户端想要禁用邻近功能但保留分配的资源以在需要时快速重新启用它们时，这非常有用。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

