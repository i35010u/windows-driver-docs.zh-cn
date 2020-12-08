---
title: 媒体 GUID
description: 媒体 GUID
keywords:
- 视频捕获 WDK AVStream，媒体
- 捕获视频 WDK AVStream，媒体
- 媒体 WDK 视频捕获
- 固定连接 WDK 视频捕获
- Guid WDK 视频捕获
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 674175dc56d816a56f726467f5fef3b3e5c7ba0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805939"
---
# <a name="medium-guids"></a>媒体 GUID

微型驱动程序必须能够支持多个设备。 此外，由于电视/广播调谐器、电视音频、横线和视频捕获组件被分为不同的内核流式处理筛选器，因此，需要使用一种方法来正确描述设备上这些组件和多个设备之间的拓扑硬件连接。 例如，两个生成但未运行的筛选器图形都必须能够共存。 微型驱动程序使用媒体来处理这些情况。 此外，筛选器图生成应用程序（如 *图形编辑*）在筛选器关系图构造期间使用媒体，以确保一个设备的筛选器正确连接到另一台设备的筛选器。 例如，一台设备的调谐器筛选器不应连接到另一台设备的横线筛选器。

微型驱动程序使用 [**KSPIN \_ 中型**](/previous-versions/ff563538(v=vs.85)) 结构描述媒体，该结构包含 GUID 数据类型成员 (**集**) 后跟两个 ULONG 成员 (**Id** 和 **标志**) ：

- 应为该 **集** 成员分配 GUID，表示拓扑硬件连接。

- 微型驱动程序必须将 **Id** 成员设置为设备实例的唯一值。

- **Flags** 成员保留供系统使用，应设置为零。

若要确保在系统中正确构造具有多个设备的筛选器图形，KSPIN 中型结构的 **集** 成员 \_ 对于每个设备实例保持不变。 但是，微型驱动程序必须将唯一值分配给 **Id** \_ 每个设备实例的 KSPIN MEDIUM 结构的 Id 成员。 如果系统中存在多个设备，则无法将 **Id** 成员设置为唯一值会导致问题。 如果系统中安装了两个设备，则微型驱动程序必须将每个设备实例的 **Id** 成员设置为不同的值。 请注意，位于同一硬件（例如调谐器和 crossbars）上的设备筛选器的 **Id** 成员必须相同。 若要确保 **id** 成员在设备实例之间不同，则在将 **id** 设置为其值之前，微型驱动程序中的全局计数器会在设备即插即用开始时间内递增计数器的值。

根据微型驱动程序遵循的内核流式处理接口 (AVStream 或 Stream 类) ，微型驱动程序必须以不同的方式指定 **Id** 成员的值：

- Stream 类微型驱动程序在处理 [**SRB \_ 获取 \_ 流 \_ 信息**](./srb-get-stream-info.md)时指定该值。

- AVStream 微型驱动程序在 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) 结构中指定值。 AVStream 微型驱动程序可通过两种不同的方式在 KSPIN \_ 描述符 EX 结构中指定值 \_ ：

    1. 提供具有全局 **Id** 计数器的静态描述符，并在 *Add* 或 *Start* 调度处理程序中调用 [**\_ KsEdit**](/windows-hardware/drivers/ddi/ks/nf-ks-_ksedit) ，以将 **Id** 成员更改为唯一值。

    1. 调用 [**KsCreateFilterFactory**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory) ，以便在 *添加* 或 *启动* 调度处理程序的过程中动态生成筛选器/pin 说明符。

微型驱动程序还必须调用特殊函数以便向 Microsoft DirectShow 注册自身，以允许应用程序使用电视/广播调谐器、电视音频和十字线筛选器自动构造筛选器图形，因为它们实际上不会为其输入和输出创建内核流式处理 pin。 当微型驱动程序注册这些筛选器时，应将 KSPIN MEDIUM 结构的 **Id** 成员设置 \_ 为唯一值。 如果微型驱动程序未将 KSPIN MEDIUM 结构的 **Id** 成员设置 \_ 为唯一值，则自动图形构建应用程序可能无法加载必要的相邻筛选器。 但在图形编辑中，手动筛选器图形生成可能仍可正常工作。

向 DirectShow 注册微型驱动程序：

- Stream 类微型驱动程序调用 [**StreamClassRegisterFilterWithNoKSPins**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisterfilterwithnokspins) 函数来向 DirectShow 注册筛选器。

- AVStream 微型驱动程序调用 [**KsRegisterFilterWithNoKSPins**](/windows-hardware/drivers/ddi/ks/nf-ks-ksregisterfilterwithnokspins) 函数来向 DirectShow 注册筛选器。

- 或者，如果微型驱动程序跟随的是 BDA 模式，并且特定 [**KSDEVICE**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice)结构下的特定 [**KSFILTER \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构的多个实例已在同一内核流式处理类别中注册，则调用 [**KsFilterFactoryUpdateCacheData**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterfactoryupdatecachedata) (或 [**BdaFilterFactoryUpdateCacheData**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdafilterfactoryupdatecachedata)) 函数向 DirectShow 注册筛选器。

\_ \_ \_ 对于 STREAM 类微型驱动程序) ，从 SRB 获取流信息 (返回的 KSPIN 中型结构 \_ ，或 \_ AVStream 微型驱动程序的 KSPIN 描述符 \_ EX () 必须与 \_ 以下属性中返回的 KSPIN MEDIUM 成员匹配：

- [**KSPROPERTY \_ 纵横 \_**](./ksproperty-crossbar-pininfo.md) [**KSPROPERTY 的 \_ \_ PININFO \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s)结构的 **中** 成员。 如果媒体不匹配，则在微型驱动程序的筛选器与关系图中的相邻筛选器之间，图形生成可能会失败。

- [**KSPROPERTY \_ 调谐器 \_ cap**](./ksproperty-tuner-caps.md)的 [**KSPROPERTY \_ 调谐器 \_ cap \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)结构的 **VideoMedium** 和 **AudioMedium** 成员。

- [**KSPROPERTY \_ TVAUDIO \_ cap**](./ksproperty-tvaudio-caps.md)的 [**KSPROPERTY \_ TVAUDIO \_ cap \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_caps_s)结构的 **InputMedium** 和 **OutputMedium** 成员。

除了正确实现媒体和中型 Guid 外，还需要遵循其他准则，以确保进程可以使用多个筛选器关系图。 在筛选器图形转换为 KSSTATE 的 **KSSTATE \_ 获取** 值之前，微型驱动程序不得锁定任何硬件资源。 这有助于确保两个生成但未运行的筛选器图形可以共存，而不会相互干扰。

有关媒体的详细信息，包括如何实现它们，请参阅 [AVStream 模拟硬件示例驱动程序 (AVSHwS) ](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)。

> [!NOTE]
> 在从 Windows 驱动程序工具包)  (的示例代码中派生新的微型驱动程序时，必须为这些媒体生成新的 GUID 值，以反映设备的独特硬件拓扑。 如果不这样做，可能会导致一台设备的媒体与为另一台设备定义的媒介发生冲突。
