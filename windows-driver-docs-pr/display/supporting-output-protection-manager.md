---
title: 支持输出保护管理器
description: 支持输出保护管理器
ms.assetid: 2c138dbd-55ca-4c71-8c8b-b2efd1ca80f2
keywords:
- COPP WDK DirectX VA，输出保护管理器
- 输出保护管理器 WDK 显示
- OPM WDK 显示
- 复制保护 WDK 显示
- 视频复制保护 WDK 显示
- 受保护的视频 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96a11c1dbe5cde248b901eeff483475d09deca6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825610"
---
# <a name="supporting-output-protection-manager"></a>支持输出保护管理器


通过输出保护管理器（OPM）设备驱动程序接口（DDI），可对由图形适配器的各种连接器输出的视频信号进行复制保护。 若要了解有关 Windows Vista 如何保护图形适配器输出内容的详细信息，请在[输出内容保护和 Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc)网站上下载内容保护文档的输出。

OPM 是[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)提供的[经过认证的输出保护协议（COPP）](copp-processing.md)的后续版本。 OPM 支持 COPP 的所有功能。 有关 COPP 功能的信息，请参阅[COPP 简介](introduction-to-copp.md)。 OPM 还支持新功能。

## <a name="opm-interface"></a>OPM 接口

**OPM ddi**在语义上类似于[COPP ddi](sample-functions-for-copp.md) ，因为对于 Windows Vista 显示器驱动程序模型，OPM 实质上是 COPP 1.1。 但是，OPM DDI 比 COPP DDI 简单得多，因为 OPM DDI 包含一组函数，而 COPP DDI 通过 DirectDraw 和 DirectX 视频加速（VA） DDI 进行映射。

如果显示微型端口驱动程序支持在应用程序和驱动程序之间传递受保护的命令、信息和状态，则 Microsoft DirectX 图形内核子系统（*Dxgkrnl*）可以成功打开驱动程序的 OPM DDI。

必须使用 OPM 接口的内核模式组件启动对显示微型端口驱动程序的[DxgkDdiQueryInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数的调用来检索接口。 指向 OPM 接口函数的指针将在[QUERY_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_query_interface)结构的接口成员指向的[DXGK_OPM_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_opm_interface)结构中返回。 此 QUERY_INTERFACE 由 DxgkDdiQueryInterface 调用中的*QueryInterface*参数指向。

以下输出保护管理器（OPM）接口函数由某些显示微型端口驱动程序实现：

* [DXGKDDI_OPM_GET_CERTIFICATE_SIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)
* [DXGKDDI_OPM_GET_CERTIFICATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)
* [DXGKDDI_OPM_CREATE_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)
* [DXGKDDI_OPM_GET_RANDOM_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)
* [DXGKDDI_OPM_SET_SIGNING_KEY_AND_SEQUENCE_NUMBERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)
* [DXGKDDI_OPM_GET_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)
* [DXGKDDI_OPM_GET_COPP_COMPATIBLE_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)
* [DXGKDDI_OPM_CONFIGURE_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)
* [DXGKDDI_OPM_DESTROY_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)

以下主题介绍了 OPM 的新功能以及如何支持和使用 OPM DDI：

[OPM 术语](opm-terminology.md)

[OPM 功能](opm-features.md)

[执行硬件功能扫描](performing-a-hardware-functionality-scan.md)

[检索 OPM DDI](retrieving-the-opm-ddi.md)

[使用 OPM DDI](using-the-opm-ddi.md)

[用 OPM 处理保护级别](handling-protection-levels-with-opm.md)

[处理显示设备的丢失](handling-the-loss-of-a-display-device.md)

[检索有关受保护的输出的信息](retrieving-information-about-a-protected-output.md)

[检索有关受保护输出的 COPP 兼容信息](retrieving-copp-compatible-information-about-a-protected-output.md)

[配置受保护的输出](configuring-a-protected-output.md)

[报告受保护的输出的状态](reporting-status-of-a-protected-output.md)

[OPM 的实现提示和要求](implementation-tips-and-requirements-for-opm.md)

 

 





