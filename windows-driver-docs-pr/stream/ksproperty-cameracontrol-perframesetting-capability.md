---
title: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能
description: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_属性中定义的 KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能属性 ID 用于获取驱动程序中的每帧功能。
ms.assetid: 9EB8AB4C-56C0-4F70-AFFE-76444FAADFF8
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CAPABILITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CAPABILITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 715305b681160e7c733ed434e56b77e5ef87c3f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842495"
---
# <a name="ksproperty_cameracontrol_perframesetting_capability"></a>KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能

\_KSPROPERTY 中定义的**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能**属性 ID [ **\_CAMERACONTROL\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property)用于获取每帧驱动程序的功能。 这是一个仅获取控件;驱动程序必须失败任何设置调用。

## <a name="usage-summary"></a>使用情况摘要

若要使用驱动程序查询每帧设置功能，请将**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能**属性控件连同数据缓冲区一起发送到该驱动程序。 在 GET 调用中，驱动程序将使用下面指定的格式布局在提供的数据缓冲区中填充每帧设置功能负载。

-   功能头（[**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)）

-   项标题（[**KSCAMERA\_PERFRAMESETTING\_CAP\_项\_标题**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)）

-   项标题（[**KSCAMERA\_PERFRAMESETTING\_CAP\_项\_标题**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)）

-   项负载（[**KSPROPERTY\_单步执行\_LONG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long)或[**KSPROPERTY\_步进\_LONGLONG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_longlong)）

功能负载必须以功能头开头。 每个功能项必须以项标题开头。 如果功能项具有有效负载，则项标头必须后跟相应的项负载。

在 GET 调用中，将先向驱动程序发送零长度缓冲区，以找出所需的数据缓冲区大小来保存整个功能负载。 作为对调用的响应，驱动程序必须返回**状态\_缓冲区\_溢出**，其中必须至少包含[**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)的大小。

下面介绍了**KSCAMERA\_PERFRAMESETTING\_CAP**在**KSCAMERA\_PERFRAMESETTING\_类型**枚举中定义的项类型上下文中的\_标头字段。 负载字段表示**KSCAMERA\_PERFRAMESETTING\_CAP 后的项负载结构\_项\_标头**结构。


**曝光时间项**  

**大小**

这是**KSCAMERA\_PERFRAMESETTING\_帽\_标头**结构的大小 + **KSPROPERTY\_单步执行**的大小，如果支持手动模式，则\_LONGLONG 结构。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_项\_公开\_时间**。

**随意**

其中包含可用标志。 此字段必须包含可通过执行 ksmedia 中定义的一个或一些标志的标志。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO       0x0000000100000000
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**负载**

如果驱动程序支持手动模式，则必须在 KSPROPERTY\_步进\_LONGLONG 中指定范围负载。SignedMinimum\\SignedMaxmum 和 KSPROPERTY\_单步执行\_LONGLONG。SteppingDelta

**闪存项**  

**大小**

这是[**KSCAMERA\_PERFRAMESETTING\_帽\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)结构的大小。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_ITEM\_类型。KSCAMERA\_PERFRAMESETTING\_项\_FLASH**

**随意**

其中包含可用标志。 此字段必须包含可通过在 ksmedia 中定义的按位或 FLASH 标志提供的标志。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_OFF                                 0x0000000000000000  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON                                  0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON_ADJUSTABLEPOWER                  0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO                                0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO_ADJUSTABLEPOWER                0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_FLASH_REDEYEREDUCTION                     0x0000000000000010
```

**负载**

闪光灯项没有有效负载。 如果 KSCAMERA\_EXTENDEDPROP\_闪存\_\_ADJUSTABLEPOWER 或 KSCAMERA\_EXTENDEDPROP\_闪存\_自动\_ADJUSTABLEPOWER 在标志中指定，则 power 参数的范围介于0到100之间。

**曝光补偿项**  

**大小**

这是**KSCAMERA\_PERFRAMESETTING\_帽\_标头**结构的大小 + **KSPROPERTY\_单\_步执行**步骤的大小（如果支持步骤）。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_ITEM\_类型。KSCAMERA\_PERFRAMESETTING\_项\_公开\_补偿**

**随意**

其中包含可用标志。 此字段必须包含可用的标志，这些标志可通过执行以下在 ksmedia 中定义的 EVCOMP 标志或在 ksmedia\_phone 中定义的自动标志来完成。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO               0x0000000100000000
#define KSCAMERA_EXTENDEDPROP_EVCOMP_SIXTHSTEP      0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_QUARTERSTEP    0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_THIRDSTEP      0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_HALFSTEP       0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_FULLSTEP       0x0000000000000010
```

**负载**

如果驱动程序仅支持 auto 模式，则不包含有效负载。 否则，必须在[**KSPROPERTY\_单步执行\_LONG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long)结构中指定范围负载。 EV 补偿的最小值和最大值为绝对 EV 补偿值，并由**KSPROPERTY\_单步执行\_长时间决定。SignedMinimum**和 KSPROPERTY\_步进\_LONG。SignedMaximum。 EV 补偿的步骤由对应于 float 的最小 EVCOMP 步骤标志的步长大小确定（例如，1/6 for KSCAMERA\_EXTENDEDPROP\_EVCOMP\_SIXTHSTEP）。

**ISO 速度项**  

**大小**

这是**KSCAMERA\_PERFRAMESETTING\_帽\_标头**结构的大小 + **KSPROPERTY\_单步执行**的大小，如果支持手动模式，则\_长结构。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_ITEM\_类型。KSCAMERA\_PERFRAMESETTING\_ITEM\_ISO**

**随意**

此字段包含可用标志。 此字段必须包含可通过执行以下操作的标志：在 ksmedia 中定义的 ISO 标志或在中定义的 ISO 标志\_。 如果支持每帧 ISO，则驱动程序必须至少支持以下功能之一，ISO\_自动和 ISO\_手动，其中 ISO\_AUTO 是必需的。 如果播发 ISO\_"手动"，则驱动程序必须在**KSPROPERTY\_单步执行\_长时间内进一步公布受支持的 ISO 速度\\max\\步骤。** 如果需要手动 iso，则必须支持 iso\_"手动"。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL    0x0080000000000000
```

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_AUTO      0x0000000000000001
```

**负载**

如果驱动程序仅支持 auto 模式，则不包含有效负载。 否则，必须在**KSPROPERTY\_单步执行\_LONG**结构中指定范围负载。 ISO 速度的最小值、最大值和阶数由**KSPROPERTY\_单步执行\_长时间决定。UnsignedMinimum**，K**SPROPERTY\_步进\_LONG。UnsignedMaximum**和**KSPROPERTY\_步进\_LONG。SteppingDelta**。 支持整数手动 ISO 的驱动程序应仅公布 ISO\_手册，其中包含支持的 ISO 速度范围（最小/最大/步骤）。 对于每帧 ISO，不支持将数字 ISO\_Xxx 预设。

**焦点项**  

**大小**

这是**KSCAMERA\_PERFRAMESETTING\_帽\_标头**结构的大小 + **KSPROPERTY\_单步\_执行长**结构的大小。

**Type**

这必须是[**KSCAMERA\_PERFRAMESETTING\_ITEM\_类型。KSCAMERA\_PERFRAMESETTING\_项\_焦点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_perframesetting_item_type#kscamera-perframesetting-item-focus)。

**随意**

其中包含可用标志。 此字段必须通过执行 ksmedis 中定义的一个按位或标记来设置。

```cpp
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**负载**

必须在 KSPROPERTY\_单步执行\_LONG 结构中指定范围负载。 镜头位置的最小值、最大值和阶数取决于**KSPROPERTY\_步进\_长。UnsignedMinimum**， **KSPROPERTY\_步进\_LONG。UnsignedMaximum**和**KSPROPERTY\_步进\_LONG。SteppingDelta**。 按照以下方式定义每帧设置焦点的行为以及它如何 interworks 全局焦点设置。

1.  镜头位置为粘滞;但不包括焦点命令。 如果在全局设置中选择了 "连续自动焦点（CAF）"，则只会为指定的帧重写 CAF 操作，并且在提供的手动焦点后 CAF 可能会移动镜头位置（可能在完全扫描之后）。

2.  除非使用 PFS 中的手动设置显式重写，否则始终假定全局焦点设置。

3.  如果没有指定手动替代，则全局 AF 为一步，并且仅适用于第一帧。

4.  除非 PFS 显式重写，否则全局 CAF 适用于所有帧。

5.  全局手动焦点设置在手动 PFS 之后不会还原（镜头位置仍然存在）。

**确认图像类型** 

**大小**

这是**KSCAMERA\_PERFRAMESETTING\_帽\_标头**结构的大小。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_ITEM\_类型。KSCAMERA\_PERFRAMESETTING\_项\_PHOTOCONFIRMATION**。

**随意**

不使用 "标志" 字段。

**负载**

此项没有有效负载。


**自定义属性项**  

**大小**

这是**KSCAMERA\_PERFRAMESETTING\_帽\_标头**结构和 GUID 大小的大小。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_ITEM\_类型。KSCAMERA\_PERFRAMESETTING\_项\_自定义**。

**随意**

不使用 "标志" 字段。

**负载**

这是自定义属性 GUID。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
