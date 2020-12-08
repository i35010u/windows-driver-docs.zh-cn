---
title: 将核心驱动程序与包感知驱动程序捆绑到一起
description: 将核心驱动程序与包感知驱动程序捆绑到一起
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c8c4d2f91e3b31f22d6173949276a5e58f2a2a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797753"
---
# <a name="bundling-the-core-driver-with-your-package-aware-driver"></a>将核心驱动程序与包感知驱动程序捆绑到一起


[展开](getting-the-updated-core-driver-package.md)Microsoft 独立更新 (MSU) 文件中包含核心驱动程序包的内容后，下一步是将核心驱动程序与包感知驱动程序捆绑在一起。

更改为包含包感知驱动程序的文件的目录，并为核心驱动程序包创建一个子目录。 这些包是特定于体系结构的，如果你要交付多体系结构驱动程序，你必须为每个体系结构都包含正确的核心驱动程序包，并为包含这些核心驱动程序包的子目录分配适当的名称。 将包含 MSU 文件的已更新核心驱动程序包子目录的内容复制到新的子目录中。 不需要进行其他更改。 不要篡改或更改已进行数字签名的核心驱动程序包。 签名将保持有效，除非更改包的内容。

 

 




