---
title: 驱动程序如何识别 32 位调用方
description: 驱动程序如何识别 32 位调用方
ms.assetid: 9bfe9024-60f1-41ad-a034-160caaaa7801
keywords:
- 32位 i/o 支持 WDK 64 位，可识别32位调用方
- 标识32位调用方
- 32位调用方标识 WDK 64 位
- 文件系统控制代码 WDK 64 位
- FSCTL WDK 64 位
- 控制代码 WDK 64 位
- I/o 控制代码 WDK 内核，64位驱动程序中的32位 i/o
- IOCTLs WDK 内核，64位驱动程序中的32位 i/o
- 调用方标识 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d39fd2acd5c5a8441766ae541e4ccff46c2b667f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187175"
---
# <a name="how-drivers-identify-32-bit-callers"></a>驱动程序如何识别 32 位调用方





驱动程序可通过两种方法来确定 IOCTL 或 FSCTL 请求的发起方是32位还是64位应用程序。 第一种是让应用程序标识自己。 第二个是让驱动程序自行决定应用程序是32位还是64位。

第一种方法涉及到在 IOCTL 或 FSCTL 控制代码中定义 "64 位" 字段。 此字段包含单个位，只为64位调用方设置。 因此，64位调用方使用一组单独的64位控制代码（其中设置了此位）来标识自身。 32位调用方使用一组类似的控制代码，其中没有设置此位。

第二种方法允许32和64位应用程序继续使用相同的 IOCTL 或 FSCTL 代码。 相反，驱动程序将通过调用 [**IoIs32bitProcess**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iois32bitprocess)来确定用户模式进程是32还是64位。

第一种方法更高效，因为驱动程序会检查位标志，而不是调用内核模式例程。 但是，第二种方法不需要对用户模式代码进行任何更改。 应使用哪种方法取决于驱动程序的要求，以及向其发送 i/o 请求的应用程序。

 

