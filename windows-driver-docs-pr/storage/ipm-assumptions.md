---
title: IPM 假设
description: IPM 假设
ms.assetid: 3c8d8121-9987-43d3-b573-4ca1d26fef7d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c99cb643e669012413b4800d423a923cc4588377
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368728"
---
# <a name="ipm-assumptions"></a>IPM 假设


从 SCSI 启动单元命令发出到 LUN 的时间在 240 秒 （4 分钟） 内完成的操作磁盘启动。

以下的 SCSI 命令 (SRB\_函数\_EXECUTE\_SCSI 操作) 应完成而无需启动磁盘。 换而言之，没有以前的 SCSI 启动单元命令是必需的。

查询

报表 LUN

微型端口驱动程序应完成所有 Srb 除 SRB\_函数\_IO\_控件、 SRB\_函数\_刷新和 SRB\_函数\_关闭时的 LUN 是在低功耗状态。

 

 




