---
title: 'HardcodedIVCNG (补充 Windows 驱动程序 CodeQL 查询) '
description: HardcodedIVCNG 补充 Windows Driver CodeQL 查询
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: c649dadcea762255ed18dcd237c8ca95e68c6132
ms.sourcegitcommit: 0e165d26ea3887d87eb41d591b8d847038a73085
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106387621"
---
# <a name="hardcodedivcng-windows-driver-codeql-query"></a>HardcodedIVCNG (Windows Driver CodeQL Query) 

## <a name="overview"></a>概述

 (IV) 的初始化向量是用于提供初始状态的加密基元的输入。 通常，IV 需要为随机或伪随机方案 (随机方案) ，但有时，IV 只需成为不可预测的或唯一的 (有状态方案) 。

随机化对于某些加密方案非常重要，目的是实现语义安全，这是一个属性，该属性重复使用同一密钥下的方案不允许攻击者推断 (加密消息可能类似) 段之间的关系。

## <a name="recommendation"></a>建议

所有对称块密码还必须与相应的初始化向量（ (IV) 根据所使用的操作模式一起使用。

如果使用的是随机方案，如 CBC，则建议使用加密的安全伪随机数生成器，如 [BCryptGenRandom](https://docs.microsoft.com/windows/win32/api/bcrypt/nf-bcrypt-bcryptgenrandom)。

## <a name="additional-details"></a>其他详细信息

此查询可在 [Microsoft GitHub CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools)中找到。  有关 Windows 驱动程序开发人员如何下载和运行 CodeQL 的详细信息，请参阅 [CodeQL 和静态工具徽标测试](./static-tools-and-codeql.md) 页。

## <a name="additional-references"></a>其他参考：

- [BCryptEncrypt 函数 (bcrypt) ](https://docs.microsoft.com/windows/win32/api/bcrypt/nf-bcrypt-bcryptencrypt)
- [BCryptGenRandom 函数 (bcrypt) ](https://docs.microsoft.com/windows/win32/api/bcrypt/nf-bcrypt-bcryptgenrandom)
- [ (维基百科) 的初始化向量 ](https://en.wikipedia.org/wiki/Initialization_vector)
