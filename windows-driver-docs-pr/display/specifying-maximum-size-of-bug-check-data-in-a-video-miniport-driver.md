---
title: 视频微型端口驱动程序中 Bug 检查数据的最大大小
description: 在视频微型端口驱动程序中指定 Bug 检查数据的最大大小
keywords:
- BugcheckDataSize
- 视频微型端口驱动程序错误-检查数据 WDK DirectX 9。0
- bug-检查数据大小 WDK DirectX 9。0
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 1f9342e5d00f43d8d4a3f4c0b9fcd7740ce81997
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840747"
---
# <a name="the-max-size-of-bug-check-data-in-a-video-miniport-driver"></a>视频微型端口驱动程序中 Bug 检查数据的最大大小


**本主题仅适用于 Microsoft Windows XP Service Pack 1 (SP1) 和更高版本。**

对于 Windows XP SP1 和 Microsoft Windows Server 2003 版本，视频微型端口驱动程序必须将 **VideoPortRegisterBugcheckCallback** 函数的 *BugcheckDataSize* 参数的值设置为不大于 0x0F20 (4000) 字节。 在 Windows Server 2003 及更高版本中， *BugcheckDataSize* 的最大值是 "最大 \_ 辅助 \_ 转储 \_ 大小" 常数。 此常量的值在低于 Windows Server 2003 的版本中可能会更改。

Windows XP SP1 DDK 文档错误地指定了 *BugcheckDataSize* 的最大值。

 

 





