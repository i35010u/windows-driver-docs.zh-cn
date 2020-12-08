---
title: 低音管理
description: 低音管理
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 041d2aad359ad9b46763d215b9f6063a096c9b44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784933"
---
# <a name="bass-management"></a>低音管理


有两种低音管理模式：转发低音管理和反向低音管理。

-   正向低音 management 筛选出音频数据流的低频率内容。 正向低音管理算法将筛选输出重定向到低音炮，或重定向到左侧和右侧的扬声器通道，具体取决于可以处理深度低音频率的通道。 此决定基于 LRBig 标志的设置。

    若要设置 LRBig 标志，用户可以使用 "控制面板" 中的 "声音小程序" 来访问 "低音管理设置" 对话框。 用户选中一个复选框以指示，例如，右前方和左左扬声器是完整范围，此操作将设置 LRBig 标志。 若要清除此标志，请单击复选框将其清除。

-   反向低音管理将信号从低音炮通道分发到其他输出通道。 该信号将定向到所有通道，或者定向到左侧和前右通道，具体取决于 LRBig 标志的设置。 将低音炮信号混合到其他通道时，此过程将使用大幅降低。

    使用的低音管理模式取决于低音炮的可用性和主要扬声器的低音处理功能。 在 Windows 中，用户通过控制面板中的 "声音" 小程序提供了此信息。

 

 




