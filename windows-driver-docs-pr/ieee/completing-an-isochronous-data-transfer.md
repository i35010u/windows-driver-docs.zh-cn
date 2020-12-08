---
title: 完成常时等量数据传输
description: 完成常时等量数据传输
keywords:
- 同步 i/o WDK IEEE 1394 总线，完成传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50e669c09d551e6097ef2149bd86b35f80120b2b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824145"
---
# <a name="completing-an-isochronous-data-transfer"></a>完成常时等量数据传输





设备不再需要传输数据后，该驱动程序必须通知总线该操作已完成，然后在设置时解除分配其所分配的同步资源。

驱动程序必须按照以下步骤进行清理：

1.  如果驱动程序已通过 [**请求 \_ ISOCH \_ 侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655) 或 [**请求 \_ ISOCH \_ 对话**](https://msdn.microsoft.com/library/windows/hardware/ff537660) 总线请求开始同步操作，则它必须发出 [**request \_ ISOCH \_ stop**](https://msdn.microsoft.com/library/windows/hardware/ff537659) 请求，通知总线驱动程序停止同步操作。

2.  仍附加到资源句柄的任何缓冲区必须使用 [**请求 \_ ISOCH \_ 分离 \_ 缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff537651) 请求进行分离。

3.  如果驱动程序已分配资源句柄，则必须通过 [**请求 \_ ISOCH \_ FREE \_**](https://msdn.microsoft.com/library/windows/hardware/ff537654) resource 请求将其解除分配。

4.  如果驱动程序已分配通道，则必须通过 [**request \_ ISOCH \_ FREE \_ 通道**](https://msdn.microsoft.com/library/windows/hardware/ff537653) 请求将其解除分配。

5.  驱动程序必须通过使用 [**请求 \_ ISOCH \_ FREE \_ 带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537652) 请求来释放已分配的所有带宽。

 

 




