---
title: Ndis 版本信息要求
description: Ndis 版本信息要求
ms.assetid: b2850077-271f-4bb6-8710-ae9415ad5eda
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18ed9eff0905c027d684da02ecd5c5da23d7f878
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554176"
---
# <a name="version-information-requirements-for-ndis"></a>Ndis 版本信息要求





NDIS 支持保证 NDIS 版本之间一致的行为的各种标头版本信息要求。 若要支持标头版本信息，NDIS 具有下列职责：

-   处理具有较低的修订的结构。 即 NDIS 检查标头信息和解释基于标头中的修订版本信息的结构。

-   函数调用将失败并返回相应的错误代码，如果驱动程序使用不正确的结构修订版本。 例如，如果 NDIS 6.30 驱动程序使用 Xxx NDIS 失败的函数调用\_修订\_1 结构时 NDIS 6.30 Xxx\_修订\_2 结构。

## <a name="related-topics"></a>相关主题


[NDIS 版本的概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






