---
title: 网络 INF 文件中的 Remove 节
description: 网络 INF 文件中的 Remove 节
ms.assetid: c9be4e98-fa35-4966-895a-aebe29f16289
keywords:
- INF 文件 WDK 网络，删除部分
- 可使用网络 INF 文件 WDK，删除部分
- 删除部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38359509414853158d6d987e99b0856cb9ac1e96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385834"
---
# <a name="remove-section-in-a-network-inf-file"></a>网络 INF 文件中的 Remove 节





**删除**支持部分**NetClient**， **NetTrans**，并且**NetService**组件而不是为**Net**组件 （适配器）。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

网络类安装程序不会不跟踪的适配器实例。 一个**删除**删除由其他适配器或适配器的多个实例共享的文件的部分可能导致这些适配器或适配器实例不起作用。
是否必须由驱动程序文件中删除**Net**组件，请使用一个跟踪的所有驱动程序的使用文件的共同安装程序。 此类共同安装程序还应跟踪的同一个设备，以及多个设备的驱动程序的多个实例。 有关共同安装程序的详细信息，请参阅[创建一个 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)。

 

 





