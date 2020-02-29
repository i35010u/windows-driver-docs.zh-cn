---
title: HID 应用程序编程接口（API）
description: 人体学接口设备（HID） API 简介。
ms.assetid: 477FF911-5A17-4EA5-9403-1D7B4E8B3BA5
keywords:
- “人机接口设备”
- HID
- 键盘
- 鼠标
- 传感器数据
- 加速感应器
- 陀螺仪
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 32617754aa2973bd1c8eac7db62b5c044c086684
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166659"
---
# <a name="hid-application-programming-interface-api"></a>HID 应用程序编程接口（API）

有三种类型的 HID Api：设备发现和设置、数据移动和报表创建/解释。

## <a name="device-discovery-and-setup"></a>设备发现和设置

这些 HID Api 用于标识 HID 设备的属性并建立与该设备的通信。 应用程序使用这些 Api 来标识顶层集合。

- [HidD\_GetAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getattributes)
- [HidD\_GetHidGuid](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_gethidguid)
- [HidD\_GetIndexedString](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getindexedstring)
- [HidD\_GetManufacturerString](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getmanufacturerstring)
- [HidD\_GetPhysicalDescriptor](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getphysicaldescriptor)
- [HidD\_GetPreparsedData](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata)
- [HidD\_GetProductString](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getproductstring)
- [HidD\_GetSerialNumberString](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getserialnumberstring)
- [HidD\_GetNumInputBuffers](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getnuminputbuffers)
- [HidD\_SetNumInputBuffers](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setnuminputbuffers)

## <a name="data-movement"></a>数据移动

这些 HID Api 用于在应用程序和所选设备之间移动数据。

- [HidD\_GetInputReport](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getinputreport)
- [HidD\_SetFeature](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setfeature)
- [HidD\_SetOutputReport](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_setoutputreport)
- [ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)
- [WriteFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)

## <a name="report-creation-and-interpretation"></a>报表创建和解释

自定义硬件的开发人员知道其设备所颁发的每个报表的大小和格式。 在这种情况下，应用程序可以将输入和输出报表缓冲区转换为结构并使用数据。

用于与公开常见功能的所有设备（例如，必须在按下播放按钮时检测的音乐应用程序）进行通信的 HID 应用程序的开发人员可能不知道 HID 报表的大小和格式。 此类别的应用程序了解某些顶级集合和某些使用情况。

若要解释从设备接收到的报表或创建要发送的报表，应用程序必须利用报表描述符来确定特定用法在报表中的位置和位置（可能为报表中的值单位）。 在这些情况下，需要进行 HID 分析。 Windows 提供了一个 HID 分析器供驱动程序和应用程序通过 Api （HidP\_\*）供驱动程序和应用程序使用，该分析器可用于发现设备支持的使用类型、确定报表中此类用法的状态，或者生成报表以更改设备中的使用状态。

这些是 HID 分析器 Api。

- [HidP\_GetButtonCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps)
- [HidP\_GetButtons](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
- [HidP\_GetButtonsEx](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
- [HidP\_GetCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getcaps)
- [HidP\_](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getdata)
- [HidP\_GetExtendedAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getextendedattributes)
- [HidP\_GetLinkCollectionNodes](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getlinkcollectionnodes)
- [HidP\_GetScaledUsageValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)
- [HidP\_GetSpecificButtonCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificbuttoncaps)
- [HidP\_GetSpecificValueCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificvaluecaps)
- [HidP\_GetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)
- [HidP\_GetUsagesEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)
- [HidP\_GetUsageValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)
- [HidP\_GetUsageValueArray](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)
- [HidP\_GetValueCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps)
- [HidP\_InitializeReportForID](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_initializereportforid)
- [HidP\_IsSameUsageAndPage](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_usage_and_page)
- [HidP\_MaxDataListLength](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxdatalistlength)
- [HidP\_MaxUsageListLength](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxusagelistlength)
- [HidP\_SetButtons](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
- [HidP\_SetData](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setdata)
- [HidP\_SetScaledUsageValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)
- [HidP\_SetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)
- [HidP\_SetUsageValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)
- [HidP\_SetUsageValueArray](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)
- [HidP\_UnsetButtons](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)
- [HidP\_UnsetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)
- [HidP\_UsageAndPageListDifference](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539824(v=vs.85))
- [HidP\_UsageListDifference](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_usagelistdifference)
