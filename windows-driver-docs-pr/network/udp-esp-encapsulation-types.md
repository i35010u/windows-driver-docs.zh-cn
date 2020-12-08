---
title: UDP-ESP 封装类型
description: UDP-ESP 封装类型
keywords:
- UDP 封装的 ESP 数据包 WDK IPsec 卸载，封装类型和子类型
- 封装 WDK UDP-ESP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f80b83390534e4ff6259236f501011b1712eed0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839429"
---
# <a name="udp-esp-encapsulation-types"></a>UDP-ESP 封装类型

\[IPsec 任务卸载功能已弃用，不应使用。\]




下图显示了在端口4500上收到的 Internet 密钥交换 (IKE) 数据包和受 ESP 保护的数据包的 UDP 封装。

![说明端口4500的基本 udp esp 封装的示意图](images/4500-encap-types.png)

请注意在 IKE 数据包中跟随 UDP 标头后的四个字节。 此零字段将从端口4500上的 UDP 封装的 ESP 数据包中区分 IKE 数据包。 ESP 标头在数据包中的此位置不会有一个非零的 ESP 标头。

### <a name="udp-esp-encapsulation-subtypes"></a>UDP-ESP 封装子类型

可以根据以下 UDP-ESP 封装子类型之一来格式化端口4500上的 ESP 数据包：

-   UDP 封装的传输。

    由 UDP 封装的 ESP 封装传输模式数据包。

-   UDP 封装的隧道。

    数据包的隧道模式部分以 UDP 方式封装。 数据包的传输模式部分不是 UDP 封装的，并且不受 ESP 保护。

-   经由 UDP 封装的隧道传输。

    数据包的隧道模式部分以 UDP 方式封装。 数据包的传输模式部分不是 UDP 封装的，而是受 ESP 保护。

-   UDP 封装的经由隧道传输。

    数据包的隧道模式部分未封装为 UDP。 数据包的传输模式部分是 UDP 封装的，并受 ESP 保护。

请注意，通过 UDP 封装的隧道的 UDP 封装的传输不是受支持的封装子类型。

下图显示了端口4500的 UDP-ESP 封装子类型。

![说明端口4500的 udp esp 封装子类型的示意图](images/4500-encap-subtypes.png)

 

 





