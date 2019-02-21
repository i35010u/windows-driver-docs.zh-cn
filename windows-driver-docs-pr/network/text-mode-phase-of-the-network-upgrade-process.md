---
title: 网络升级过程的文本模式阶段
description: 网络升级过程的文本模式阶段
ms.assetid: 4878e0ae-194a-459c-bebf-75259b1eed2d
keywords:
- 网络组件升级，WDK 阶段
- 升级网络组件 WDK，阶段
- 文本模式阶段 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f567b813392aead3e22c1c1be5ecb9c40bb28060
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541385"
---
# <a name="text-mode-phase-of-the-network-upgrade-process"></a>网络升级过程的文本模式阶段





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

安装程序中去除从应答文件的所有注释，并将应答文件写入到下名称 $Winnt$.inf 的 System32 目录。 然后在系统启动到 GUI 模式下安装程序。 在文本模式阶段期间不发生任何特定于网络的处理。

 

 





