---
title: IRP 处理示例
description: IRP 处理示例
ms.assetid: 1bf555c7-87fd-43c2-ab74-aa6f9133f808
keywords:
- Irp WDK 内核，处理示例
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e260d544a234589bf768669db5902d5685adfbc4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524996"
---
# <a name="irp-processing-examples"></a>IRP 处理示例





以下部分介绍如何在两个原型驱动程序中可能会处理 Irp。 一个是大容量存储设备的最低级别驱动程序的原型。 另一个是中间级别的原型*镜像驱动程序*，它们将上面的存储设备驱动程序堆栈中的最低级别驱动程序存在。 （镜像驱动程序复制到多个驱动程序的所有写入请求和备用连接形式读取在重复驱动器之间的请求）。

[处理 Irp 到最低级别的驱动程序](processing-irps-in-a-lowest-level-driver.md)

[中间级驱动程序中处理 Irp](processing-irps-in-an-intermediate-level-driver.md)

若要了解有关创建和发送 Irp 的详细信息，请参阅[不同的方法来处理 Irp – 备忘单](https://go.microsoft.com/fwlink/?linkid=834615)。

