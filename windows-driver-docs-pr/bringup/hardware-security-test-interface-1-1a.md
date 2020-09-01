---
title: 硬件安全测试接口 (HSTI) 1.1a
description: 硬件安全测试接口 (HSTI) 1.1a
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: f6699a713e5347ad67357af870cfebdadc7b922a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189001"
---
# <a name="hardware-security-test-interface-hsti-11a"></a>硬件安全测试接口 (HSTI) 1.1a


HSTI 指定了适用于专有平台安全技术的标准测试接口，这些技术强制实施安全启动承诺 (例如，SPI 闪存或 eMMC 分区锁定，正确配置 SMM 配置、正确配置 Intel Boot Guard 等) 。 硅和 BIOS 供应商指定并实现在发布固件中随附的必要测试用例作为内置自检。

将测试接口包含在固件中后，知识丰富的使用者可以验证是否存在固件安全功能。

以下 Windows 版本中包含对 HSTI 的支持：

-   Windows Server Technical Preview 2016

-   Windows 10 版本1607及更高版本


## <a name="related-resources"></a>相关资源

[硬件安全可测试性规范](/windows-hardware/test/hlk/testref/hardware-security-testability-specification)