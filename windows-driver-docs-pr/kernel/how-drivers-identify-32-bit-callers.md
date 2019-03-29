---
title: 驱动程序如何识别 32 位调用方
description: 驱动程序如何识别 32 位调用方
ms.assetid: 9bfe9024-60f1-41ad-a034-160caaaa7801
keywords:
- 32 位 I/O 支持 WDK 64 位、 32 位的调用方标识
- 确定调用方 32 位
- 32 位调用方标识 WDK 64 位
- 文件系统控制代码 WDK 64 位
- FSCTL WDK 64 位
- 控制代码 WDK 64 位
- I/O 控制代码 WDK 内核，在 64 位驱动程序中的 32 位 I/O
- Ioctl WDK 内核，在 64 位驱动程序中的 32 位 I/O
- 调用方标识 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1c0e5aa033197d94d201c2afbaf5c67d2114a54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576270"
---
# <a name="how-drivers-identify-32-bit-callers"></a>驱动程序如何识别 32 位调用方





有两种方法确定一个 IOCTL 或 FSCTL 请求的发起方是一个 32 位或 64 位应用程序的驱动程序。 首先，为应用程序来标识自身。 第二个是应用程序是 32 位或 64 位驱动程序以自行决定的。

第一种方法涉及到定义 IOCTL 或 FSCTL 控制代码中的"64 位"字段。 此字段包含的 64 位的调用方设置的单个位。 因此 64 位的调用方标识自身使用一组单独的 64 位控制代码将设置此位。 32 位的调用方使用一组类似的控制代码将不设置此位。

第二种方法允许 32 位和 64 位应用程序以继续使用相同的 IOCTL 或 FSCTL 代码。 相反，该驱动程序确定用户模式进程是否通过调用为 32 位或 64 位[ **IoIs32bitProcess**](https://msdn.microsoft.com/library/windows/hardware/ff549372)。

第一种方法是更高效，因为该驱动程序检查而不是调用内核模式例程的位标志。 但是，第二种方法需要对用户模式代码的任何更改。 应使用何种技术取决于您的驱动程序将 I/O 请求发送到它的应用程序的要求。

 

 




