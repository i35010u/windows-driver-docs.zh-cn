---
title: NDIS 的版本信息要求
description: NDIS 的版本信息要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fbcccdc4783a4383a0ebd48bc6c7ddc2c923669
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802273"
---
# <a name="version-information-requirements-for-ndis"></a>NDIS 的版本信息要求





NDIS 支持各种标头版本信息要求，确保 NDIS 版本之间的行为一致。 为了支持标头版本信息，NDIS 具有以下职责：

-   处理较低修订版本的结构。 也就是说，NDIS 检查标头信息，并基于标头中的修订信息解释结构。

-   如果驱动程序使用不正确的结构修订，则函数调用失败，并返回相应的错误代码。 例如，如果 ndis 6.30 的驱动程序在 \_ \_ 有 Ndis 6.30 Xxx 版本2的结构时使用 Xxx 版本1结构，则 ndis 将无法调用函数 \_ \_ 。

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






