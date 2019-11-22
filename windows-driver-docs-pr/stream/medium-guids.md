---
title: 媒体 GUID
description: 媒体 GUID
ms.assetid: 4209952c-0ba5-4359-b612-91529a0a46f1
keywords:
- 视频捕获 WDK AVStream，媒体
- 捕获视频 WDK AVStream，媒体
- 媒体 WDK 视频捕获
- 固定连接 WDK 视频捕获
- Guid WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e15b7a2bb052fd8b31789a122d94b7a1cb8dbadb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838039"
---
# <a name="medium-guids"></a>媒体 GUID


微型驱动程序必须能够支持多个设备。 此外，因为电视/广播调谐器、电视音频、横线和视频捕获组件被分隔到不同的内核流式处理筛选器中，所以必须使用一种方法来正确描述这些组件在设备以及多个设备上。 例如，两个生成但未运行的筛选器图形都必须能够共存。 微型驱动程序使用媒体来处理这些情况。 此外，筛选器图生成应用程序（如*图形编辑*）在筛选器关系图构造期间使用媒体，以确保一个设备的筛选器正确连接到另一台设备的筛选器。 例如，一台设备的调谐器筛选器不应连接到另一台设备的横线筛选器。

微型驱动程序使用[**KSPIN\_MEDIUM**](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))结构来描述媒体，其中包含 GUID 数据类型成员（**Set**），后跟两个 ULONG 成员（**Id**和**Flags**）：

-   应为该**集**成员分配 GUID，表示拓扑硬件连接。

-   微型驱动程序必须将**Id**成员设置为设备实例的唯一值。

-   **Flags**成员保留供系统使用，应设置为零。

为了确保在系统中正确构造具有多个设备的筛选器图形，KSPIN\_中结构的**集**成员对于每个设备实例保持不变。 但是，微型驱动程序必须为每个设备实例的 KSPIN\_MEDIUM 结构的**Id**成员分配唯一值。 如果系统中存在多个设备，则无法将**Id**成员设置为唯一值会导致问题。 如果系统中安装了两个设备，则微型驱动程序必须将每个设备实例的**Id**成员设置为不同的值。 请注意，位于同一硬件（例如调谐器和 crossbars）上的设备筛选器的**Id**成员必须相同。 若要确保**id**成员在设备实例之间不同，则在将**id**设置为其值之前，微型驱动程序中的全局计数器会在设备即插即用开始时间内递增计数器的值。

根据微型驱动程序遵循的内核流式处理接口（AVStream 或 Stream 类），微型驱动程序必须以不同的方式指定**Id**成员的值：

-   Stream 类微型驱动程序在处理[**SRB\_获取\_流\_信息**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)时指定该值。

-   AVStream 微型驱动程序在[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构中指定值。 AVStream 微型驱动程序可通过两种不同的方法在 KSPIN\_描述符\_EX 结构中指定值：

    1.  提供具有全局**Id**计数器的静态描述符，并在*添加*或*启动*调度处理程序过程中调用[ **\_KsEdit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-_ksedit) ，以将**Id**成员更改为唯一值。
    2.  调用[**KsCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory) ，以便在*添加*或*启动*调度处理程序的过程中动态生成筛选器/pin 说明符。

微型驱动程序还必须调用特殊函数以便向 Microsoft DirectShow 注册自己，以允许应用程序使用电视/广播调谐器、电视音频和十字线筛选器自动构造筛选器图形，因为它们实际上不会创建用于输入和输出的内核流式处理 pin。 当微型驱动程序注册这些筛选器时，应将 KSPIN\_中结构的**Id**成员设置为唯一值。 如果微型驱动程序未将 KSPIN\_中结构的**Id**成员设置为唯一值，则自动图形构建应用程序可能无法加载必要的相邻筛选器。 但在图形编辑中，手动筛选器图形生成可能仍可正常工作。

向 DirectShow 注册微型驱动程序：

-   Stream 类微型驱动程序调用[**StreamClassRegisterFilterWithNoKSPins**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisterfilterwithnokspins)函数来向 DirectShow 注册筛选器。

-   AVStream 微型驱动程序调用[**KsRegisterFilterWithNoKSPins**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksregisterfilterwithnokspins)函数来向 DirectShow 注册筛选器。

-   或者，如果微型驱动程序遵循了 BDA 模式，并且特定[**KSDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice)结构下的特定[**KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构的多个实例已在同一内核流式处理类别中注册，则调用[**KsFilterFactoryUpdateCacheData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterfactoryupdatecachedata) （或[**BdaFilterFactoryUpdateCacheData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdafilterfactoryupdatecachedata)）函数来向 DirectShow 注册筛选器。

从 SRB 中返回的 KSPIN\_MEDIUM 结构\_获取\_流\_信息（对于 Stream 类为微型驱动程序），或 KSPIN\_描述符\_EX （对于 AVStream 微型驱动程序）必须与 KSPIN\_MEDIUM 成员匹配在以下属性中返回：

-   KSPROPERTY 的**中型**成员[ **\_纵横比\_PININFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s)的[**KSPROPERTY\_纵横比\_PININFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-pininfo)的结构。 如果媒体不匹配，则在微型驱动程序的筛选器与关系图中的相邻筛选器之间，图形生成可能会失败。

-   [**KSPROPERTY\_调谐器\_cap\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)\_结构的**VideoMedium**和**AudioMedium**成员[ **\_cap cap**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-caps)。

-   [**KSPROPERTY\_TVAUDIO\_cap\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_caps_s)结构的**InputMedium**和**OUTPUTMEDIUM**成员[ **\_KSPROPERTY\_cap**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-caps)。

除了正确实现媒体和中型 Guid 外，还需要遵循其他准则，以确保进程可以使用多个筛选器关系图。 在筛选器图形转换为**KSSTATE\_获取**KSSTATE 的值之前，微型驱动程序不得锁定任何硬件资源。 这有助于确保两个生成但未运行的筛选器图形可以共存，而不会相互干扰。

有关媒体的详细信息，包括如何实现它们，请参阅[AVStream 模拟硬件示例驱动程序（AVSHwS）](https://go.microsoft.com/fwlink/p/?linkid=256083)。

**注意**  ：从 Windows 驱动程序工具包中的示例代码派生新的微型驱动程序时，必须为媒体生成新的 GUID 值，以反映设备的独特硬件拓扑。 如果不这样做，可能会导致一台设备的媒体与为另一台设备定义的媒介发生冲突。

 

 

 




