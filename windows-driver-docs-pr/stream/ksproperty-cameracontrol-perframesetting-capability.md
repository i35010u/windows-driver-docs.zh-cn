---
title: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能
description: KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_KSPROPERTY 中定义的功能属性 ID\_CAMERACONTROL\_PERFRAMESETTING\_属性用于获取每个帧从驱动程序的功能。
ms.assetid: 9EB8AB4C-56C0-4F70-AFFE-76444FAADFF8
keywords:
- KSPROPERTY_CAMERACONTROL_PERFRAMESETTING_CAPABILITY 流式处理媒体设备
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
ms.openlocfilehash: 605f647216d8ca92bf86ab16caf3892ef323b965
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575201"
---
# <a name="kspropertycameracontrolperframesettingcapability"></a>KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能

**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能**中定义的属性 ID [ **KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property)用于获得驱动程序的每个框架功能。 这是 GET 的唯一控件;该驱动程序必须失败的任何集调用。

## <a name="usage-summary"></a>使用情况摘要

每个帧设置功能使用驱动程序，查询**KSPROPERTY\_CAMERACONTROL\_PERFRAMESETTING\_功能**属性控制发送到数据缓冲区以及该驱动程序。 在 GET 调用，该驱动程序将填充每个帧设置功能有效负载中使用下面指定的格式布局提供的数据缓冲区。

-   功能标头 ([**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header))

-   项标头 ([**KSCAMERA\_PERFRAMESETTING\_CAP\_项\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header))

-   项标头 ([**KSCAMERA\_PERFRAMESETTING\_CAP\_项\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header))

-   项有效负载 ([**KSPROPERTY\_单步执行\_长**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_stepping_long)或者[ **KSPROPERTY\_单步执行\_LONGLONG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_stepping_longlong))

功能有效负载必须以功能标头开头。 每个功能项必须开头的项标头。 如果功能的项具有一个有效负载，项标头后面必须有相应的项有效负载。

在 GET 调用中，一个零长度缓冲区是先发送到该驱动程序来找出所需的数据缓冲区大小来保存整个功能有效负载。 在响应调用，则驱动程序必须返回**状态\_缓冲区\_OVERFLOW**使用所需的功能的缓冲区大小必须至少为的大小[ **KSCAMERA\_PERFRAMESETTING\_CAP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)。

以下是的说明**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**中的项类型的上下文中的字段定义**KSCAMERA\_PERFRAMESETTING\_项\_类型**枚举。 负载字段表示后的项有效负载结构**KSCAMERA\_PERFRAMESETTING\_CAP\_项\_标头**结构。


**项的暴露时间**  

**大小**

这是的大小**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**结构 + 的大小**KSPROPERTY\_单步执行\_LONGLONG**结构，如果支持手动模式。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_项\_暴露\_时间**。

**标志**

这包含可用的标志。 通过执行按位或的 ksmedia.h 中定义的标志，此字段必须包含可用的标志。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO       0x0000000100000000
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**Payload**

如果该驱动程序支持手动模式下，必须 KSPROPERTY 中指定的范围有效负载\_单步执行\_LONGLONG。Bounds.SignedMinimum\\SignedMaxmum 和 KSPROPERTY\_单步执行\_LONGLONG。SteppingDelta

**Flash 项**  

**大小**

这是的大小[ **KSCAMERA\_PERFRAMESETTING\_CAP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)结构。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_项\_类型。KSCAMERA\_PERFRAMESETTING\_项\_FLASH**

**标志**

这包含可用的标志。 通过执行按位或的 ksmedia.h 中定义下面的闪存标志，此字段必须包含可用的标志。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_OFF                                 0x0000000000000000  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON                                  0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON_ADJUSTABLEPOWER                  0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO                                0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO_ADJUSTABLEPOWER                0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_FLASH_REDEYEREDUCTION                     0x0000000000000010
```

**Payload**

闪存项没有有效负载。 如果 KSCAMERA\_EXTENDEDPROP\_闪存\_ON\_ADJUSTABLEPOWER 或 KSCAMERA\_EXTENDEDPROP\_FLASH\_自动\_中指定 ADJUSTABLEPOWER标志，power 参数是介于 0 到 100 之间。

**曝光补偿项**  

**大小**

这是的大小**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**结构 + 的大小**KSPROPERTY\_单步执行\_长时间**结构，如果受支持的步骤。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_项\_类型。KSCAMERA\_PERFRAMESETTING\_项\_暴露\_补偿**

**标志**

这包含可用的标志。 此字段必须包含通过执行按位可用的标志，或者的 EVCOMP ksmedia.h 或自动标记中定义以下标志定义如下 ksmedia\_phone.h。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO               0x0000000100000000
#define KSCAMERA_EXTENDEDPROP_EVCOMP_SIXTHSTEP      0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_QUARTERSTEP    0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_THIRDSTEP      0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_HALFSTEP       0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_FULLSTEP       0x0000000000000010
```

**Payload**

如果驱动程序支持仅 auto 模式，则不包含有效负载。 否则，必须在指定的范围有效负载[ **KSPROPERTY\_单步执行\_长**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_stepping_long)结构。 最小和最大值为 EV 补偿是绝对 EV 补偿值，将根据**KSPROPERTY\_单步执行\_长。Bounds.SignedMinimum**和 KSPROPERTY\_单步执行\_长。Bounds.SignedMaximum。 EV 补偿步骤由对应于一个浮点数的最小 EVCOMP 步骤标志的步骤大小 (例如，1/6 为 KSCAMERA\_EXTENDEDPROP\_EVCOMP\_SIXTHSTEP)。

**ISO 速度项**  

**大小**

这是的大小**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**结构 + 的大小**KSPROPERTY\_单步执行\_长时间**结构，如果支持手动模式。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_项\_类型。KSCAMERA\_PERFRAMESETTING\_项\_ISO**

**标志**

此字段包含可用的标志。 此字段必须包含可用的标志，通过执行按位或的定义如下 ksmedia.h 和 ksmedia 中的 ISO 标志\_phone.h。 如果支持每个帧 ISO，则该驱动程序必须支持至少一个以下功能，ISO\_自动和 ISO\_手动中的 ISO\_自动是必需的。 如果 ISO\_手动播发、 驱动程序必须进一步播发的受支持的 ISO 速度最小值\\最大\\中的步骤**KSPROPERTY\_单步执行\_长。ISO\_手动**如果需要手动 ISO，则必须支持。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL    0x0080000000000000
```

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_AUTO      0x0000000000000001
```

**Payload**

如果驱动程序支持仅 auto 模式，则不包含有效负载。 否则，必须在指定的范围有效负载**KSPROPERTY\_单步执行\_长**结构。 Min、 max 和 ISO 速度的步骤将根据**KSPROPERTY\_单步执行\_长。Bounds.UnsignedMinimum**，K**SPROPERTY\_单步执行\_长。Bounds.UnsignedMaximum**，并**KSPROPERTY\_单步执行\_长。Bounds.SteppingDelta**。 驱动程序支持整数手动 ISO 应只播发 ISO\_受支持的 ISO 速度本手册的范围 （最小值/最大/步骤）。 数值 ISO\_Xxx 预设不支持的每个帧 ISO。

**焦点项**  

**大小**

这是的大小**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**结构 + 的大小**KSPROPERTY\_单步执行\_长时间**结构。

**Type**

这必须是[ **KSCAMERA\_PERFRAMESETTING\_项\_类型。KSCAMERA\_PERFRAMESETTING\_项\_焦点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_perframesetting_item_type#kscamera-perframesetting-item-focus)。

**标志**

这包含可用的标志。 此字段必须通过执行按位或在 ksmedis.h 下面定义的标志的设置。

```cpp
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**Payload**

必须在 KSPROPERTY 中指定的范围有效负载\_单步执行\_长时间结构。 Min、 max 和可重用功能区位置的步骤将根据**KSPROPERTY\_单步执行\_长。Bounds.UnsignedMinimum**， **KSPROPERTY\_单步执行\_长。Bounds.UnsignedMaximum**，并**KSPROPERTY\_单步执行\_长。SteppingDelta**。 每个帧设置焦点和它如何与全局焦点设置 interworks 的行为的定义，如下所示。

1.  可重用功能区位置是粘滞;但不是焦点命令。 如果已在全局设置中选择持续自动聚焦 （自助餐厅），自助餐厅操作仅对指定的帧中被重写和自助餐厅将可能提供手动焦点后移动 （有可能后全面扫描） 的可重用功能区位置。

2.  除非显式重写使用 PFS 中手动设置始终假定全局焦点设置。

3.  全局 AF 是单步，只适用于第一个帧，如果未不指定任何手动重写。

4.  除非显式重写由 PFS，全局自助餐厅适用于所有帧。

5.  全局手动焦点设置不还原之后手动 PFS （可重用功能区位置保持） 信息。

**确认图像类型** 

**大小**

这是的大小**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**结构。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_项\_类型。KSCAMERA\_PERFRAMESETTING\_项\_PHOTOCONFIRMATION**。

**标志**

不使用标志字段。

**Payload**

为此项目没有有效负载。


**自定义属性项**  

**大小**

这是的大小**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**结构 + GUID 的大小。

**Type**

这必须是**KSCAMERA\_PERFRAMESETTING\_项\_类型。KSCAMERA\_PERFRAMESETTING\_项\_自定义**。

**标志**

不使用标志字段。

**Payload**

这是自定义属性的 GUID。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
