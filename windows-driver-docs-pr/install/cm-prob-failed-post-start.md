---
title: CM_PROB_FAILED_POST_START
description: CM_PROB_FAILED_POST_START
keywords:
- CM_PROB_FAILED_POST_START
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3343e180659540d1caf8a1237b60d3d83bd64f3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783148"
---
# <a name="code-43---cm_prob_failed_post_start"></a>代码 43 - CM_PROB_FAILED_POST_START

此设备管理器错误消息指示驱动程序已报告设备故障。

## <a name="error-code"></a>错误代码

43

### <a name="display-message"></a>显示消息

"Windows 已停止此设备，因为它报告了问题。  (代码 43) "

### <a name="recommended-resolution"></a>推荐的解决方案

卸载并重新安装该设备。

控制设备的驱动程序之一告诉操作系统设备在响应 IRP_MN_QUERY_PNP_DEVICE_STATE 时出现故障。

## <a name="for-driver-developers"></a>面向驱动程序开发人员

驱动程序使设备的 [设备状态失效](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate) ，并在生成的查询设备状态中使设备堆栈 [PNP_DEVICE_FAILED](../kernel/irp-mn-query-pnp-device-state.md)报告。

如果该驱动程序是一个 WDF 驱动程序，则作为失败的设备的报告可能会间接地由调用 [**WdfDeviceSetFailed**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed) 的 wdf 驱动程序或从 WDF 回调返回错误引起。 有关详细信息，请参阅 [报告设备故障](../wdf/reporting-device-failures.md)。
