---
title: 媒体验证
description: 媒体验证
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 文件系统，介质验证
- 媒体验证 WDK 文件系统
- 磁盘死亡攻击 WDK 文件系统
- 验证 media WDK 文件系统
- 可移动媒体验证 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96adadaad2827f932a2b8146c085edac7f9f9c7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828017"
---
# <a name="media-validation"></a>媒体验证


## <span id="ddk_media_validation_if"></span><span id="DDK_MEDIA_VALIDATION_IF"></span>


在开发支持可移动媒体 (FASTFAT 的文件系统时，需要考虑的主要问题，例如) 阻止 "磁盘死亡" 攻击。 实现文件系统时，驱动程序必须防止恶意的格式不正确的结构，因为任何人都可以将可移动磁盘插入 (CD-ROM、DVD-ROM 或 u 盘，例如) 到系统中。

 

 




