---
title: HID 应用程序编程接口 (API)
description: 人体学接口设备简介 (HID) API。
keywords:
- “人机接口设备”
- HID
- 键盘
- mice
- 传感器数据
- 加速感应器
- 陀螺仪
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: ef0e9b60445eca195bf7dae19aeffb34d96623ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818455"
---
# <a name="hid-application-programming-interface-api"></a>HID 应用程序编程接口 (API)

有三种类型的 HID Api：设备发现和设置、数据移动和报表创建/解释。

## <a name="device-discovery-and-setup"></a>设备发现和设置

这些 HID Api 用于标识 HID 设备的属性并建立与该设备的通信。 应用程序使用这些 Api 来标识顶层集合。

- [HidD \_ GetAttributes](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getattributes)
- [HidD \_ GetHidGuid](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_gethidguid)
- [HidD \_ GetIndexedString](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getindexedstring)
- [HidD \_ GetManufacturerString](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getmanufacturerstring)
- [HidD \_ GetPhysicalDescriptor](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getphysicaldescriptor)
- [HidD \_ GetPreparsedData](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata)
- [HidD \_ GetProductString](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getproductstring)
- [HidD \_ GetSerialNumberString](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getserialnumberstring)
- [HidD \_ GetNumInputBuffers](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getnuminputbuffers)
- [HidD \_ SetNumInputBuffers](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setnuminputbuffers)

## <a name="data-movement"></a>数据移动

这些 HID Api 用于在应用程序和所选设备之间移动数据。

- [HidD \_ GetInputReport](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport)
- [HidD \_ SetFeature](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setfeature)
- [HidD \_ SetOutputReport](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setoutputreport)
- [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)
- [WriteFile](/windows/win32/api/fileapi/nf-fileapi-writefile)

## <a name="report-creation-and-interpretation"></a>报表创建和解释

自定义硬件的开发人员知道其设备所颁发的每个报表的大小和格式。 在这种情况下，应用程序可以将输入和输出报表缓冲区转换为结构并使用数据。

用于与公开常见功能的所有设备进行通信的 HID 应用程序开发人员 (例如，必须检测何时按下 "播放" 按钮的音乐应用程序) 可能不知道 HID 报表的大小和格式。 此类别的应用程序了解某些顶级集合和某些使用情况。

若要解释从设备接收到的报表或创建要发送的报表，应用程序必须利用报表描述符来确定报表中是否存在特定的使用情况，并 (在报表中可能) 值单位。 在这些情况下，需要进行 HID 分析。 Windows 提供了一个 HID 分析器供驱动程序和应用程序通过 Api (HidP \_ \*) 使用，该分析器可用于发现设备支持的使用类型、确定报表中此类用法的状态，或者生成报表以更改设备中的使用状态。

这些是 HID 分析器 Api。

- [HidP \_ GetButtonCaps](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps)
- [HidP \_ GetButtons](./hdpi-h-macros.md)
- [HidP \_ GetButtonsEx](./hdpi-h-macros.md)
- [HidP \_ GetCaps](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getcaps)
- [HidP \_](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getdata)
- [HidP \_ GetExtendedAttributes](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getextendedattributes)
- [HidP \_ GetLinkCollectionNodes](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getlinkcollectionnodes)
- [HidP \_ GetScaledUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)
- [HidP \_ GetSpecificButtonCaps](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificbuttoncaps)
- [HidP \_ GetSpecificValueCaps](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificvaluecaps)
- [HidP \_ GetUsages](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)
- [HidP \_ GetUsagesEx](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)
- [HidP \_ GetUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)
- [HidP \_ GetUsageValueArray](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)
- [HidP \_ GetValueCaps](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps)
- [HidP \_ InitializeReportForID](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_initializereportforid)
- [HidP \_ IsSameUsageAndPage](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_usage_and_page)
- [HidP \_ MaxDataListLength](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxdatalistlength)
- [HidP \_ MaxUsageListLength](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxusagelistlength)
- [HidP \_ SetButtons](./hdpi-h-macros.md)
- [HidP \_ SetData](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setdata)
- [HidP \_ SetScaledUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)
- [HidP \_ SetUsages](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)
- [HidP \_ SetUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)
- [HidP \_ SetUsageValueArray](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)
- [HidP \_ UnsetButtons](./hdpi-h-macros.md)
- [HidP \_ UnsetUsages](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)
- [HidP \_ UsageAndPageListDifference](/previous-versions/windows/hardware/drivers/ff539824(v=vs.85))
- [HidP \_ UsageListDifference](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_usagelistdifference)
