---
title: 将标注注册到筛选器引擎
description: 将标注注册到筛选器引擎
ms.assetid: a5bade33-e3d1-4e1d-8503-51485097046e
keywords:
- Windows 筛选平台标注驱动程序 WDK，初始化
- 标注驱动程序 WDK Windows 筛选平台，初始化
- 初始化标注驱动程序 WDK Windows 筛选平台
- 注册标注 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc64928542df427f8b26a4762db913c01f7e1717
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212011"
---
# <a name="registering-callouts-with-the-filter-engine"></a>将标注注册到筛选器引擎


标注驱动程序创建设备对象后，它可以使用筛选器引擎注册其标注。 标注驱动程序可以随时使用筛选器引擎注册其标注，即使筛选器引擎当前未运行也是如此。 若要使用筛选器引擎注册标注，标注驱动程序将调用 [**FwpsCalloutRegister0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0) 函数。 例如：

```C++
// Prototypes for the callout's callout functions
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    IN OUT FWPS_CLASSIFY_OUT0  *classifyOut
    );

NTSTATUS NTAPI
 NotifyFn(
 IN FWPS_CALLOUT_NOTIFY_TYPE notifyType,
    IN const GUID  *filterKey,
    IN const FWPS_FILTER0  *filter
    );

VOID NTAPI
 FlowDeleteFn(
    IN UINT16  layerId,
    IN UINT32  calloutId,
    IN UINT64  flowContext
    );

// Callout registration structure
const FWPS_CALLOUT0 Callout =
{
 { ... }, // GUID key identifying the callout
  0,       // Callout-specific flags (none set here)
 ClassifyFn,
 NotifyFn,
 FlowDeleteFn
};

// Variable for the run-time callout identifier
UINT32 CalloutId;

NTSTATUS
 DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  PDEVICE_OBJECT deviceObject;
  NTSTATUS status;

  ...

 status =
 FwpsCalloutRegister0(
 deviceObject,
      &Callout,
      &CalloutId
      );

  ...

 return status;
}
```

如果对 [**FwpsCalloutRegister0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0) 函数的调用成功，则最后一个参数指向的变量将包含该标注的运行时标识符。 此运行时标识符对应于为标注键指定的 GUID。

单个标注驱动程序可以实现多个标注。 如果标注驱动程序实现了多个标注，则它会对每个标注调用 [**FwpsCalloutRegister0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0) 函数，以便为每个标注注册筛选器引擎。

## <a name="related-topics"></a>相关主题


[classifyFn](/windows-hardware/drivers/ddi/_netvista/)

 

