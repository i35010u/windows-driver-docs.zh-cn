---
title: 验证新式待机系统的驱动程序更新
description: 本主题介绍如何验证针对新式待机系统的驱动程序更新。
ms.topic: article
ms.date: 12/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 190104c91ed63d6de6646ce6c4ccad4859644522
ms.sourcegitcommit: ac28dd2a921c25796d19572a180b88e460420488
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2021
ms.locfileid: "101682266"
---
# <a name="validating-driver-updates-for-modern-standby-systems"></a>验证新式待机系统的驱动程序更新 

当驱动程序更新将发布到[新式待机](/windows-hardware/design/device-experiences/modern-standby-basic-test-scenarios)系统时，请确保驱动程序的电源管理与新式待机兼容，并且不会对移动外形规格系统的电池寿命或桌面外形规格系统的电源效率产生负面影响，这一点至关重要。 

如果驱动程序更新是针对新式待机系统的，则必须至少在一个[支持新式待机的系统](/windows-hardware/design/device-experiences/overview-of-modern-standby-validation#verifying-if-a-system-is-modern-standby-capable)上执行所有测试和验证。 这应包括任何 HLK 测试和通常用于验证特定驱动程序更新的其他测试套件。 

建议在各种新式待机系统和操作系统版本上进行测试，因为硬件、固件、驱动程序和操作系统的组合会影响电源管理和电池寿命。 如果驱动程序更新也以传统睡眠 (S3) 系统为目标，则应同时对至少一个 S3 系统执行验证，但最好应对多个该系统执行验证。 

安装更新后的驱动程序之前，应通过运行 HLK 测试套件（即在测试系统上自动生成的 HLK 播放列表）来确认系统的稳定性。 如果驱动程序的现有版本导致 XHC/EHC 控制器下的某个 USB 设备或 I2C 控制器下的某个 I2C 设备故障，则在重新运行 HLK 测试套件之前，可通过设备管理器暂时禁用相应的设备。 禁用设备可能会导致某些 HLK 测试失败，例如，未能满足新式待机基本要求测试中的 DRIPS 要求，或者 DFx 系统验证测试失败；但是，测试结果的其余部分应表明平台通常是稳定的，并且能够进入和退出新式待机。 确认系统稳定性后，可以通过安装的设备管理器和更新的驱动程序来重新启用已禁用的设备。 

安装更新的驱动程序后，系统必须通过[交流电源](/windows-hardware/test/hlk/testref/c0c51f07-5b17-4b26-a7ce-bfc9e7611dac)和[直流电源](/windows-hardware/test/hlk/testref/c0c51f07-5b17-4b26-a7ce-bfc9e7611ddc)的新式待机基本要求测试，确保系统仍然能够进入低功耗状态并快速恢复待机状态。 需要新式待机系统才能在发布之前通过这些测试，因此请务必确保驱动程序更新不会导致回归。 建议在执行此测试之前在系统上执行休眠转换。

系统还必须通过 [PoFx (DFx) 导向型系统验证测试](/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)，此测试可验证系统上支持 DFx 所需的设备在其驱动程序中是否有必要的支持。 对于在驱动程序更新中需要 DFx 支持的设备，请务必确保未从设备中删除该支持。 有关 DFx 的详细信息，请参阅[导向型电源管理框架简介](../kernel/introduction-to-the-directed-power-management-framework.md)。 建议在执行此测试之前在系统上执行休眠转换。

接下来，系统必须通过[设备基础测试](../devtest/device-fundamentals-tests.md)。 在所有上述测试都已运行之后，系统必须通过 HLK [使用驱动程序验证程序的并发压力进行以运行时电源为中心的压力测试](/windows-hardware/test/hlk/testref/dfa7f945-7b63-4693-a555-0f38f33c971c)和[使用驱动程序验证程序的并发压力进行新式待机压力测试](/windows-hardware/test/hlk/testref/ae264d13-307b-452b-b5fc-4d9098ea22f1)，确保系统可以在设备 I/O 后进行运行时电源管理转换和新式待机转换，而不会出现错误。
