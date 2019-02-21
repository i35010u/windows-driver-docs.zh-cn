---
title: 确定视频 Stream 停滞的原因
description: 确定视频 Stream 停滞的原因
ms.assetid: 959c2295-1ec3-48b0-aed9-93a81378372f
keywords:
- 内核调试，流式处理视频流停滞，导致
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f596aa7a30ae7730711c649b96b158cd07e6dd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541565"
---
# <a name="determining-the-cause-of-a-video-stream-stall"></a>确定视频 Stream 停滞的原因


有两个视频流停滞的基本原因：

-   **挂起。** 用户模式线程或内核模式线程不是由驱动程序被释放。

-   **停滞。** 这是问题的与流式处理路径中的组件的结果。 一些可能的用途包括：
    -   捕获驱动程序尚未完成数据包。 在这种情况下，驱动程序组件或硬件可能停止的源。
    -   捕获驱动程序已完成的数据包。 在这种情况下，缓冲区可能会停止编解码器或其他下游组件中。

如果可以重现此问题，附加调试器此时来确定这是实际的原因。

**若要确定问题是否挂起**

1.  将用户模式下调试程序附加到应用程序并查找被阻止的用户模式线程。

2.  确定应用程序是否有响应。 可以暂停在关系图？ 可以停止在关系图？ 如果停止并重新启动在关系图，则不会流式处理重启？

3.  如果应用程序无响应，尝试通过使用任务管理器中结束的任务。 如果此操作失败，则内核模式下挂起。

**若要确定问题是否停滞**

1.  确定这些示例图中的位置。 这可以在本地或在内核模式调试会话。

2.  确定是否在下游流动示例。 如果可以再现中的 bug [GraphEdit](https://go.microsoft.com/fwlink/p/?linkid=9230)，中间的筛选器置于关系图以显示示例。

3.  确定名为处理例程。 这可以通过附加内核模式调试程序和此例程中设置断点。

 

 





