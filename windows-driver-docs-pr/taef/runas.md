---
title: RunAs
description: RunAs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad2ae0e4305fecefce255b264943a3f4d2b9c5b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806593"
---
# <a name="runas"></a>RunAs

TAEF 提供了一种机制，用于以本地系统或在低完整性过程中执行提升、受限制的测试。

## <a name="prerequisites"></a>先决条件

- [Te](te-service.md) 必须在计算机上安装并运行服务，以便从非提升的进程运行提升的测试，从提升的进程运行未提升的测试，或者将测试作为本地系统运行。

## <a name="runas-types"></a>RunAs 类型

TAEF 支持以下 RunAs 类型，这些类型通过测试元数据或命令提示符指定。

- [RunAs Elevated](runas-elevated.md)
- [RunAs LowIL](runas-lowil.md)
- [RunAs Restricted](runas-restricted.md)
- [RunAs System](runas-system.md)
