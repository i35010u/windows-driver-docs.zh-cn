---
title: KSPROPERTY \_ CAMERACONTROL \_ PERFRAMESETTING \_
description: '\_ \_ \_ KSPROPERTY CAMERACONTROL PERFRAMESETTING 属性中定义的 KSPROPERTY CAMERACONTROL PERFRAMESETTING 功能属性 \_ ID \_ \_ 用于获取驱动程序中的每帧功能。'
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
ms.openlocfilehash: 0bc3a0308b37be25eccb574751024a6f05f6e19b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185721"
---
# <a name="ksproperty_cameracontrol_perframesetting_capability"></a>KSPROPERTY \_ CAMERACONTROL \_ PERFRAMESETTING \_

[**KSPROPERTY \_ CAMERACONTROL \_ PERFRAMESETTING \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_perframesetting_property)中定义的**KSPROPERTY \_ CAMERACONTROL \_ PERFRAMESETTING \_ 功能**属性 ID 用于获取驱动程序中的每帧功能。 这是一个仅获取控件;驱动程序必须失败任何设置调用。

## <a name="usage-summary"></a>使用情况摘要

若要使用驱动程序查询每帧设置功能，请将 **KSPROPERTY \_ CAMERACONTROL \_ PERFRAMESETTING \_ 功能** 属性控件连同一个数据缓冲区一起发送到该驱动程序。 在 GET 调用中，驱动程序将使用下面指定的格式布局在提供的数据缓冲区中填充每帧设置功能负载。

-   功能头 ([**KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)) 

-   项标题 ([**KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 项 \_ 标题**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)) 

-   项标题 ([**KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 项 \_ 标题**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)) 

-   项负载 ([**KSPROPERTY \_ 步进 \_ 长**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long) 或 [**KSPROPERTY \_ 单步执行 \_ LONGLONG**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_longlong)) 

功能负载必须以功能头开头。 每个功能项必须以项标题开头。 如果功能项具有有效负载，则项标头必须后跟相应的项负载。

在 GET 调用中，将先向驱动程序发送零长度缓冲区，以找出所需的数据缓冲区大小来保存整个功能负载。 为响应调用，驱动程序必须返回 **状态 \_ 缓冲区 \_ 溢出** ，其所需的容量缓冲区大小必须至少为 [**KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)的大小。

下面是在**KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 类型**枚举中定义的项类型上下文中的**KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 标头**字段的说明。 负载字段表示 **KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 项 \_ 标头** 结构之后的项负载结构。


**曝光时间项**  

**大小**

这是 **KSCAMERA \_ PERFRAMESETTING \_ 帽 \_ 标头** 结构的大小 + **KSPROPERTY \_ 步进 \_ LONGLONG** 结构的大小（如果支持 "手动" 模式）。

**类型**

这必须是 **KSCAMERA \_ PERFRAMESETTING \_ ITEM \_ 曝露 \_ TIME**。

**标记**

其中包含可用标志。 此字段必须包含可通过执行 ksmedia 中定义的一个或一些标志的标志。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO       0x0000000100000000
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**有效负载**

如果驱动程序支持手动模式，则必须在 KSPROPERTY 步进 LONGLONG 中指定范围负载 \_ \_ 。SignedMinimum \\ SignedMaxmum 和 KSPROPERTY \_ 单步执行 \_ LONGLONG。SteppingDelta

**闪存项**  

**大小**

这是 [**KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header) 结构的大小。

**类型**

这必须是 **KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 类型。KSCAMERA \_ PERFRAMESETTING \_ 项 \_ FLASH**

**标记**

其中包含可用标志。 此字段必须包含可通过在 ksmedia 中定义的按位或 FLASH 标志提供的标志。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_OFF                                 0x0000000000000000  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON                                  0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_FLASH_ON_ADJUSTABLEPOWER                  0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO                                0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_FLASH_AUTO_ADJUSTABLEPOWER                0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_FLASH_REDEYEREDUCTION                     0x0000000000000010
```

**有效负载**

闪光灯项没有有效负载。 如果 \_ \_ 在 flags 中指定 KSCAMERA EXTENDEDPROP flash \_ ON \_ ADJUSTABLEPOWER 或 KSCAMERA \_ EXTENDEDPROP \_ flash \_ AUTO \_ ADJUSTABLEPOWER，则 power 参数的范围介于0到100之间。

**曝光补偿项**  

**大小**

如果支持步骤，这就是 **KSCAMERA \_ PERFRAMESETTING \_ 帽 \_ 标头** 结构的大小 + **KSPROPERTY \_ 单步 \_ ** 结构的大小。

**类型**

这必须是 **KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 类型。KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 公开 \_ 补偿**

**标记**

其中包含可用标志。 此字段必须包含通过在 ksmedia 中定义下面定义的 EVCOMP 标志或在 ksmedia 的中定义的自动标志来提供的 \_ 标志。

```cpp
#define KSCAMERA_PERFRAMESETTING_AUTO               0x0000000100000000
#define KSCAMERA_EXTENDEDPROP_EVCOMP_SIXTHSTEP      0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_QUARTERSTEP    0x0000000000000002  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_THIRDSTEP      0x0000000000000004  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_HALFSTEP       0x0000000000000008  
#define KSCAMERA_EXTENDEDPROP_EVCOMP_FULLSTEP       0x0000000000000010
```

**有效负载**

如果驱动程序仅支持 auto 模式，则不包含有效负载。 否则，必须在 [**KSPROPERTY \_ 步进 \_ 长**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long) 结构中指定范围负载。 EV 补偿的最小值和最大值为绝对 EV 补偿值，并由 **KSPROPERTY \_ 步进 \_ 长时间决定。SignedMinimum** 和 KSPROPERTY \_ 步进 \_ 长。SignedMaximum。 EV 补偿的步骤取决于与 float (（例如，1/6 for KSCAMERA \_ EXTENDEDPROP \_ EVCOMP SIXTHSTEP) 相对应的最小 EVCOMP 步骤标志的步长大小 \_ 。

**ISO 速度项**  

**大小**

这是 **KSCAMERA \_ PERFRAMESETTING \_ 帽 \_ 标头** 结构的大小 + **KSPROPERTY \_ 步进 \_ 长** 结构的大小（如果支持 "手动" 模式）。

**类型**

这必须是 **KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 类型。KSCAMERA \_ PERFRAMESETTING \_ ITEM \_ ISO**

**标记**

此字段包含可用标志。 此字段必须包含可用的标志，这些标志可通过执行以下在 ksmedia 和 ksmedia 中定义的 ISO \_ 标志。 如果支持每帧 ISO，则驱动程序必须至少支持以下功能之一： ISO \_ 自动和 iso \_ 手动，其中 iso \_ auto 是必需的。 如果播发了 ISO \_ 手册，驱动程序必须 \\ \\ 在 **KSPROPERTY \_ 步进 \_ 长时间内进一步公布受支持的 ISO 速度最小值步骤。如果 \_ ** 需要手动 iso，则必须支持 iso 手册。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL    0x0080000000000000
```

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_AUTO      0x0000000000000001
```

**有效负载**

如果驱动程序仅支持 auto 模式，则不包含有效负载。 否则，必须在 **KSPROPERTY \_ 步进 \_ 长** 结构中指定范围负载。 ISO 速度的最小值、最大值和阶数由 **KSPROPERTY \_ 步进 \_ 长时间决定。UnsignedMinimum**，K**SPROPERTY \_ 步进 \_ 长。UnsignedMaximum**和 **KSPROPERTY \_ 步进 \_ 长。SteppingDelta**。 支持整数手动 ISO 的驱动程序应仅公布 ISO \_ 手册，其中包含支持的 iso 速度范围 (min/max/step) 。 \_每帧 iso 不支持数字 iso Xxx 预设。

**焦点项**  

**大小**

这是 **KSCAMERA \_ PERFRAMESETTING \_ 帽 \_ 标头** 结构的大小 + **KSPROPERTY \_ 单步 \_ 长** 结构的大小。

**类型**

这必须是 [**KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 类型。KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 焦点**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_perframesetting_item_type#kscamera-perframesetting-item-focus)。

**标记**

其中包含可用标志。 此字段必须通过执行 ksmedis 中定义的一个按位或标记来设置。

```cpp
#define KSCAMERA_PERFRAMESETTING_MANUAL     0x0000000200000000
```

**有效负载**

范围负载必须在 KSPROPERTY \_ 单步执行的 \_ 长结构中指定。 镜头位置的最小值、最大值和阶数从 **KSPROPERTY \_ 步进 \_ 长时间决定。UnsignedMinimum**， **KSPROPERTY \_ 步进 \_ 长。UnsignedMaximum**和 **KSPROPERTY \_ 步进 \_ 长。SteppingDelta**。 按照以下方式定义每帧设置焦点的行为以及它如何 interworks 全局焦点设置。

1.  镜头位置为粘滞;但不包括焦点命令。 如果在全局设置中选择了 "连续自动焦点 (CAF") ，则仅为指定的帧重写 CAF 操作，并且 CAF 在提供手动焦点后可能会移动镜头位置， (可能会在完全扫描) 之后移动镜头位置。

2.  除非使用 PFS 中的手动设置显式重写，否则始终假定全局焦点设置。

3.  如果没有指定手动替代，则全局 AF 为一步，并且仅适用于第一帧。

4.  除非 PFS 显式重写，否则全局 CAF 适用于所有帧。

5.  "全局手动焦点" 设置不会在手动 PFS 后恢复 (镜头位置保持) 。

**确认图像类型** 

**大小**

这是 **KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 标头** 结构的大小。

**类型**

这必须是 **KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 类型。KSCAMERA \_ PERFRAMESETTING \_ ITEM \_ PHOTOCONFIRMATION**。

**标记**

不使用 "标志" 字段。

**有效负载**

此项没有有效负载。


**自定义属性项**  

**大小**

这是 **KSCAMERA \_ PERFRAMESETTING \_ 帽 \_ 标头** 结构的大小 + GUID 大小。

**类型**

这必须是 **KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 类型。KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 自定义**。

**标记**

不使用 "标志" 字段。

**有效负载**

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