---
title: UMDF 设置（仅供测试）选项卡
description: 本主题详细说明 WDF 验证程序的 UMDF 设置 (测试仅) 页面。
ms.assetid: cce75c2e-fc93-4c17-9560-aef55451528b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63d1c1e86052c60e6e41b0e7fb54ef382ba6bad0
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384801"
---
# <a name="umdf-settings-test-use-only-tab"></a>UMDF 设置（仅供测试）选项卡


本主题详细说明 WDF 验证程序的 **UMDF 设置 (测试仅) ** 页面。 在此页上，你可以更改设置，以帮助使用一个或多个用户模式驱动程序框架 (UMDF) 驱动程序来测试整个系统。

将这些设置用于测试目的。 完成测试后，请单击 " **还原默认值** " 按钮。 否则，计算机可能会显著降低性能。

![umdf 设置的屏幕截图 (测试仅使用) 选项卡](images/wdfverifier-tab4.png)

默认情况下， [UMDF 内录音机 (IFR) ](../wdf/using-the-framework-s-event-logger.md) 存储在非分页内存中，因此在发生系统崩溃时可以保留日志。 但是，在极少数情况下，可能需要在非分页内存中释放空间。 例如，你可能会对具有多个 UMDF 驱动程序的系统进行压力测试，而 [设备池](../wdf/using-device-pooling-in-umdf-drivers.md) 处于关闭状态，而非分页内存则为高级。 您可以通过选择 " **使用分页池** " 框来获取较小的可用非分页内存量。

此外，有时，驱动程序验证程序之类的分析工具可能会降低 CPU 密集型测试中的系统性能，即使驱动程序没有任何错误，默认 UMDF 超时也会触发这些测试。 在这种情况下，增加超时值可能会减少此类型的意外超时。

**警告**  
使用这些选项可大大降低捕获或诊断 UMDF 驱动程序故障的可能性，因此应仅在需要时使用它们。 它们更可能用于测试整体系统。

 

 

