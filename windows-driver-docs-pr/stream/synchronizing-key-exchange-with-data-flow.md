---
title: 与数据流同步密钥交换
description: 与数据流同步密钥交换
ms.assetid: 54abc258-d26a-4d42-a5aa-712cdae76b6d
keywords:
- DVD 解码器微型驱动程序 WDK，版权保护
- 解码器微型驱动程序 WDK DVD，版权保护
- 版权保护的 WDK DVD 解码器
- 密钥交换的 WDK DVD 解码器
- 解密 WDK DVD 解码器
- 加密 WDK DVD 解码器
- 加密 WDK DVD 解码器
- DVD decrypters WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a46dd2a8bacef749819c0878a2a5fc780e1d0a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523797"
---
# <a name="synchronizing-key-exchange-with-data-flow"></a>与数据流同步密钥交换





密钥交换过程可能会开始处理前一密钥中的所有数据之前。 此示例将从设置到主程序标题上某些电影设置的尾部标题的转换中。 没有在标志**TypeSpecificFlags**的成员[ **KSSTREAM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567138)的每个数据包的结构。 此标志**KS\_AM\_UseNewCSSKey**，其定义中*ksmedia.h*。 它表示紧随该标头的数据样本是新的标题项适用的第一个数据示例。

如果解密器可以处理新的密钥交换时在仍使用旧密钥，DVD 解码器微型驱动程序应处理密钥交换，因为它会接收属性。 如果解密器必须等待，直到所有影片数据需要以前的密钥已处理，则解密器保存为 SRB**设置**属性。 解密器使用[ **KS\_DVDCOPY\_设置\_复制\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567639)使用参数的结构**KS\_DVDCOPYSTATE\_初始化**或**KS\_DVDCOPYSTATE\_初始化\_标题**直到其收到**KS\_AM\_UseNewCSSKey**上连接到它的所有流的标志。 此后，DVD 解码器微型驱动程序处理直到该点接收的所有数据包。 这可以防止对数据使用不正确的项。

 

 




