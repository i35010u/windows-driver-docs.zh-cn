---
title: 低音管理
description: 低音管理
ms.assetid: b3fb6fcf-cf86-4627-912e-253b5864ab9e
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: a4988c1da2bb73257ec52e0e1a17031fe924e706
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566679"
---
# <a name="bass-management"></a>低音管理


有两种低音管理模式： 正向低音管理及反向低音管理。

-   正向低音管理筛选出低频率流内容的音频数据。 正向低音管理算法与低音或到 front 左和 front 右扬声器的渠道，具体取决于可以处理深度低音频率的通道筛选的输出重定向。 此决定基于 LRBig 标志的设置。

    若要设置 LRBig 标志，用户使用声音小程序在 Control Panel 中访问低音管理设置对话框。 用户选择一个复选框以指示，例如，前端右和从前端左扬声器完整范围，此操作设置 LRBig 标志。 若要清除此标志，请单击复选框以将其清除。

-   反向低音管理将分发到其他输出通道从低音通道信号。 信号是定向到的所有通道或前端左和 front 右通道，具体取决于 LRBig 标志的设置。 到其他通道混合低音信号时，此过程将使用大量提升减少。

    使用低音管理模式依赖于了重低音喇叭的可用性和主要发言人的低音处理功能。 在 Windows 中，用户提供此信息通过控制面板中的声音小程序。

 

 




