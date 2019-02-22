---
title: 支持输出保护管理器
description: 支持输出保护管理器
ms.assetid: 2c138dbd-55ca-4c71-8c8b-b2efd1ca80f2
keywords:
- COPP WDK DirectX VA，输出保护管理器
- 输出 Protection Manager WDK 显示
- OPM WDK 显示
- 复制保护 WDK 显示
- 视频复制保护 WDK 显示
- 受保护视频 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de880c8af0af882a0d5df662f77301b7f1784d31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543869"
---
# <a name="supporting-output-protection-manager"></a>支持输出保护管理器


输出保护管理器 (OPM) 设备驱动程序接口 (DDI) 使视频信号的图形适配器的各种连接器输出复制保护。 若要了解有关 Windows Vista 如何保护内容的详细信息的图形适配器输出，请下载处的输出内容保护文档[输出内容保护和 Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc)网站。

OPM 是继[认证的输出保护协议 (COPP)](copp-processing.md)的[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)提供。 OPM 支持所有 COPP 的功能。 有关 COPP 的功能的信息，请参阅[简介 COPP](introduction-to-copp.md)。 OPM 还支持新功能。

## <a name="opm-interface"></a>OPM 接口

**OPM DDI**语义上类似于[COPP DDI](sample-functions-for-copp.md)因为 OPM 是实质上是 COPP 1.1 for Windows Vista 显示器驱动程序模型。 但是，OPM DDI 是 COPP DDI 比简单得多，因为 OPM DDI COPP DDI 映射通过 DirectDraw 和 DirectX 视频加速 (VA) DDI 时包含一组函数。

如果显示微型端口驱动程序支持应用程序和驱动程序，Microsoft DirectX 图形内核子系统之间的受保护的命令、 信息和状态传递 (*Dxgkrnl.sys*) 可以成功打开驱动程序的 OPM DDI。

必须使用 OPM 界面的内核模式组件开始显示微型端口驱动程序调用[DxgkDdiQueryInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数以检索接口。 返回指向 OPM 接口函数的指针[DXGK_OPM_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_opm_interface)结构的接口成员[QUERY_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_query_interface)结构指向。 指向此 QUERY_INTERFACE *QueryInterface* DxgkDdiQueryInterface 调用中的参数。

某些显示微型端口驱动程序实现以下的输出保护管理器 (OPM) 接口函数：

* [DXGKDDI_OPM_GET_CERTIFICATE_SIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)
* [DXGKDDI_OPM_GET_CERTIFICATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)
* [DXGKDDI_OPM_CREATE_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)
* [DXGKDDI_OPM_GET_RANDOM_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)
* [DXGKDDI_OPM_SET_SIGNING_KEY_AND_SEQUENCE_NUMBERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)
* [DXGKDDI_OPM_GET_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)
* [DXGKDDI_OPM_GET_COPP_COMPATIBLE_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)
* [DXGKDDI_OPM_CONFIGURE_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)
* [DXGKDDI_OPM_DESTROY_PROTECTED_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)

以下主题介绍 OPM 以及如何支持和使用 OPM DDI 的新功能：

[OPM 术语](opm-terminology.md)

[OPM 功能](opm-features.md)

[执行硬件功能扫描](performing-a-hardware-functionality-scan.md)

[检索 OPM DDI](retrieving-the-opm-ddi.md)

[使用 OPM DDI](using-the-opm-ddi.md)

[处理与 OPM 的保护级别](handling-protection-levels-with-opm.md)

[处理显示设备的丢失](handling-the-loss-of-a-display-device.md)

[检索有关受保护的输出的信息](retrieving-information-about-a-protected-output.md)

[检索有关受保护的一个输出 COPP 兼容信息](retrieving-copp-compatible-information-about-a-protected-output.md)

[配置受保护的输出](configuring-a-protected-output.md)

[报告的受保护的输出的状态](reporting-status-of-a-protected-output.md)

[实现技巧和 OPM 的要求](implementation-tips-and-requirements-for-opm.md)

 

 





