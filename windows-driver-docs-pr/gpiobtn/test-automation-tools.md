---
title: 测试自动化工具
description: GPIO 测试自动化使用 MITT 平台。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2a0b533078aa45950211e2b67e69dc6d7b61cf38
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790651"
---
# <a name="test-automation-tools"></a>测试自动化工具


GPIO 测试自动化使用 MITT 平台。

若要开始，请参阅 [MITT 中的 GPIO 测试](../spb/gpio-tests-in-mitt.md)。 下载安装程序，解压缩其内容，并阅读 **自述** 文件以获取该工具的一般概述。

若要将该工具连接到受测系统，需要 GPIO 按钮和指示器引脚。 安装主板并安装其相关程序包后，可以通过以下任一方式使用它：

-   针对 GPIO 按钮和指示器方案运行现有的自动化测试。
-   使用模式生成器来探索其他方案。

测试二进制文件是 MITT 工具安装程序的一部分。 若要开始测试，请按照 MITT 文档的 "运行 GPIO 自动化" 一节中的说明进行操作。

MITT 工具可以直接生成用于模拟) 各种按钮按下操作的等效项的 GPIO impulses (按下，按住按钮按下并松开按钮。 这些测试是基于 [SimpleIo](../wdtf/provided-wdtf-simpleio-plug-ins.md)的，可以检测到问题，例如在电源转换后出现不同步的指示器。

**注意**  
MITT 平台可以轻松容纳自定义的输入模式。 有关如何生成这些文件的说明，请参阅 MITT 自述文件。

 

