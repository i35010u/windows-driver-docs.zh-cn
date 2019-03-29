---
title: 将核心驱动程序与包感知驱动程序捆绑到一起
description: 将核心驱动程序与包感知驱动程序捆绑到一起
ms.assetid: 72e29f79-4e71-4aa8-929f-eefdebfe4835
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9de28136f4b3baa54cc479d36417c35ba8d23aa3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577015"
---
# <a name="bundling-the-core-driver-with-your-package-aware-driver"></a>将核心驱动程序与包感知驱动程序捆绑到一起


检查完[展开](getting-the-updated-core-driver-package.md)包含核心驱动程序包的 Microsoft 独立更新 (MSU) 文件的内容下, 一步是捆绑包识别驱动程序使用的核心驱动程序。

将更改为包含识别包的驱动程序文件的目录，并为核心驱动程序包创建一个子目录。 这些包是特定于体系结构，并且如果交付多体系结构驱动程序必须包括每个体系结构的正确核心驱动程序包并将相应的名称分配到包含这些核心驱动程序包的子目录。 将复制到新的子目录中包含的 MSU 文件更新的核心驱动程序程序包子目录的内容。 不需要进行任何其他更改。 不要篡改或更改核心驱动程序包进行了数字签名。 除非您更改包的内容，该签名会保持有效。

 

 




