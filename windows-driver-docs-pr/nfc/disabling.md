---
title: 禁用 NFP
description: 订阅、 发布和状态，可以暂时禁用客户端。
ms.assetid: 94BE6D24-60AD-45BD-AF2D-388022114975
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38c4d2f1538c0564ea64fc373dcca6ec572ddd3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370537"
---
# <a name="disabling-nfp"></a>禁用 NFP


订阅、 发布和状态，可以暂时禁用客户端。

暂时禁用针对订阅、 发布和状态显示通过发送[ **IOCTL\_NFP\_禁用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_disable)句柄。 当客户端想要禁用的邻近性功能，但保留分配快速重新启用它们时所需的资源时，这很有用。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

