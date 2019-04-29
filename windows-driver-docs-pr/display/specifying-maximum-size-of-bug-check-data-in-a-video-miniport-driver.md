---
title: 视频微型端口驱动程序中 Bug 检查数据的最大大小
description: 指定视频微型端口驱动程序中的 Bug 检查数据的最大大小
ms.assetid: 1644fe85-b5f5-44b5-96b7-258f43607171
keywords:
- BugcheckDataSize
- 微型端口驱动程序 bug 检查数据 WDK DirectX 9.0
- bug 检查数据大小 WDK DirectX 9.0
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 5505f45a4d2bb32dd9c3394a8da1aa383fcf71a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376041"
---
# <a name="the-max-size-of-bug-check-data-in-a-video-miniport-driver"></a>视频微型端口驱动程序中 Bug 检查数据的最大大小


**本主题仅适用于 Microsoft Windows XP Service Pack 1 (SP1) 和更高版本。**

微型端口驱动程序必须设置为值*BugcheckDataSize*的参数**VideoPortRegisterBugcheckCallback**函数，以便不应超过 0x0F20 (4000) 字节适用于 Windows XP SP1 和Microsoft Windows Server 2003 版本。 在 Windows Server 2003 和更高版本中，将最大值为*BugcheckDataSize*是最高\_辅助\_转储\_大小常量。 此常量的值晚于 Windows Server 2003 版本中可能会更改。

Windows XP SP1 DDK 文档错误地指定的最大值*BugcheckDataSize*。

 

 





