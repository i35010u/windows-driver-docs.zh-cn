---
title: 媒体验证
description: 媒体验证
ms.assetid: 609ac09b-88be-49a6-8b87-9fd453c21446
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 的文件系统，媒体验证
- 媒体验证 WDK 的文件系统
- 磁盘死机紫攻击 WDK 的文件系统
- 正在验证媒体 WDK 的文件系统
- 可移动介质验证 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d36445f9fc02dc36ddfecd2db26ed2dc5b269e90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540621"
---
# <a name="media-validation"></a>媒体验证


## <span id="ddk_media_validation_if"></span><span id="DDK_MEDIA_VALIDATION_IF"></span>


开发支持可移动介质 (例如 FASTFAT) 的文件系统时主要考虑因素防范"磁盘死机紫"攻击。 因为任何人都可以插入可移动磁盘时实现文件系统，该驱动程序必须防止对恶意格式不正确的结构 (CD-ROM，DVD ROM 或 USB 闪存内存磁盘，例如) 到系统。

 

 




