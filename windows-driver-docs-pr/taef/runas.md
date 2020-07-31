---
title: RunAs
description: RunAs
ms.assetid: 47183A50-513C-4bc5-8DC4-33065323F584
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a8be4e9412f4c06df88ed2133d9425fed43f56
ms.sourcegitcommit: f63852446e614c985a65f599cdfe788bdb0c6089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425731"
---
# <a name="runas"></a>RunAs

TAEF 提供了一种机制，用于以本地系统或在低完整性过程中执行提升、受限制的测试。

## <a name="prerequisites"></a>先决条件

- [Te](te-service.md)必须在计算机上安装并运行服务，以便从非提升的进程运行提升的测试，从提升的进程运行未提升的测试，或者将测试作为本地系统运行。

## <a name="runas-types"></a>RunAs 类型

TAEF 支持以下 RunAs 类型，这些类型通过测试元数据或命令提示符指定。

- [RunAs Elevated](runas-elevated.md)
- [RunAs LowIL](runas-lowil.md)
- [RunAs Restricted](runas-restricted.md)
- [RunAs System](runas-system.md)
