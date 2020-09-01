---
title: 入门指南-适用于3D 打印机的 Microsoft 标准驱动程序
description: 用于3D 打印机的 Microsoft 标准驱动程序使开发人员能够轻松地使其打印机与 Windows 10 兼容。
ms.assetid: DAFC5B26-09BA-483C-B964-1DA96E77765F
ms.date: 05/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1cc425f3d91d2bcb184917f7a877787b87a6d00c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184515"
---
# <a name="getting-started-guide---microsoft-standard-driver-for-3d-printers"></a>入门指南-适用于3D 打印机的 Microsoft 标准驱动程序

用于3D 打印机的 Microsoft 标准驱动程序使开发人员能够轻松地使其打印机与 Windows 10 兼容。 使用 Microsoft OS 描述符的任何打印机都可以被识别为兼容的3D 打印机。 本文将介绍如何创建固件，使设备能够通过 Windows 10 识别为3D 打印机并传达其打印功能。

## <a name="introduction"></a>简介

Microsoft 标准版驱动程序免除了从独立的硬件供应商 (Ihv 编写自己的驱动程序的负担，) 希望其3D 打印机与 Windows 10 兼容。 可识别 Microsoft OS 描述符的 Windows 版本使用控制请求来检索信息，并使用它来安装和配置设备，而无需任何用户交互。

在 Windows 10 上运行3D 打印机的一般过程包括以下步骤：

1. **兼容 ID**。 独立硬件供应商 (IHV) 必须在打印机的固件中包含 "3D Print" 兼容 ID。 这允许将设备识别为3D 打印机。

2. **标准驱动程序**。 设备接通电源后，Windows 更新会下载3D 打印标准版驱动程序，并将当前设备检测为使用默认配置的3D 打印机。

3. **扩展属性说明符**。 3D 打印机的几个基本配置将作为标准驱动程序的一部分提供。 因此，开发人员可以选择与其3D 打印机匹配的基本配置。 根据选择基本配置，开发人员可以覆盖某些属性以更好地匹配其3D 打印机，并将它们包含在新的固件中。

4. **即插即**用。 将固件刻录到3D 打印机的闪存后，只要用户将其插入到 Windows 10 计算机中，就会自动下载标准驱动程序，并使用开发人员选择的自定义打印功能。

在以下部分中，我们将使用具体的示例来演示其中的每个步骤。

有关详细信息，请参阅 [MICROSOFT OS 描述符](/previous-versions/gg463179(v=msdn.10))。

## <a name="compatible-id"></a>兼容 ID

若要指定当前使用3D 打印机的 Windows 操作系统，则必须使用正确的兼容 ID。 Microsoft [OS 描述符](/previous-versions/gg463179(v=msdn.10))中提供了 MICROSOFT 兼容 ID 列表。

三维打印机的兼容 ID 如下表中所示：

| 兼容 ID | 与子兼容的 ID | 说明 |
| --- | --- | --- |
| "3DPRINT"<br><br> (0x33 0x44 0x50 0x52 0x49 0x4E 0x54 0x00)  | 多种多样 | MS3DPRINT G-代码打印机 |

在3D 打印机固件中包含的头文件中，IHV 必须指定兼容的 ID，如下所示：

```cpp
#define MS3DPRINT_CONFIG_SIZE 232

#define MS3DPRINT_OSP_SIZE (4+4+2+0x20+4+MS3DPRINT_CONFIG_SIZE)

#define MS3DPRINT_XPROP_SIZE (4+2+2+2+MS3DPRINT_OSP_SIZE)

#define SIZE_TO_DW(__size)                \
        ((uint32_t)__size) & 0xFF,        \
        (((uint32_t)__size)>>8) & 0xFF,   \
        (((uint32_t)__size)>>16) & 0xFF,  \
        (((uint32_t)__size)>>24) & 0xFF

// CompatibleID and SubCompatibleID
static const uint8_t PROGMEM ms3dprint_descriptor[40] = {
    0x28, 0x00, 0x00, 0x00,                          // dwLength
    0x00, 0x01,                                      // bcdVersion
    0x04, 0x00,                                      // wIndex
    0x01,                                            // bCount
    0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,        // RESERVED
    0x00,                                            // bFirstInterfaceNumber
    0x01,                                            // RESERVED
    '3', 'D', 'P', 'R', 'I', 'N', 'T', 0x00,         // compatibleID ("3DPRINT")
                                                 // subCompatibleID
    0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00   /*        */  
,
    0x00, 0x00, 0x00, 0x00, 0x00, 0x00               // RESERVED
};
```

以上代码中的此行是3D 打印机的兼容 ID：

`'3', 'D', 'P', 'R', 'I', 'N', 'T', 0x00,         // compatibleID ("3DPRINT")`

对于此特定配置，Ihv 可以编译其固件并闪存设备。 然后，当设备接通电源时，3D 打印标准驱动程序将自动从 Windows 更新下载。

在此阶段，打印机使用的是标准驱动程序默认配置，默认配置使用的参数在文件 StandardGCode.xml 中的文件夹% SYSTEMROOT% \\ System32 MS3DPrint 中可访问 \\ 。 此外，开发人员可以选择使用不同的基础配置，在同一文件夹% SYSTEMROOT% System32 MS3DPrint 中提供了一个基本配置列表 \\ \\ 。 随着新的3D 打印机在市场上出现，此列表会定期填充新的配置。

## <a name="extended-properties-os-feature-descriptor"></a>扩展属性 OS 功能描述符

如上一节所述，Ihv 有权访问多个基本配置。 这样做的优点是可以将必须存储在打印机闪存中的信息量降到最低。 开发人员可以检查提供的基本配置，并选择最靠近其打印机的基本配置。 在此示例中，我们将选择 SD 卡基本配置，并用以下参数替代某些属性：

| 参数 | 值 |
| --- | --- |
| Job3DOutputAreaWidth | 250000 |
| Job3DOutputAreaDepth | 260000 |
| Job3DOutputAreaHeight | 270000 |
| Filamentdiameter | 2850 |

有关这些参数的详细信息，请参阅[ (MSI 下载) ](https://go.microsoft.com/fwlink/p/?LinkId=394375)文档中的*MS3DPrint 标准 G 代码 Driver.docx*文档。

若要指定要使用的基本配置以及要重写的参数，开发人员必须通过扩展属性 OS 功能描述符来指定它，如下所示：

```cpp
// Modifiers to the base configuration
static const uint8_t PROGMEM ms3dprint_properties_descriptor[] = {
    SIZE_TO_DW(MS3DPRINT_XPROP_SIZE),                   // dwLength
    0x00, 0x01,                                         // bcdVersion
    0x05, 0x00,                                         // wIndex
    0x01, 0x00,                                         // wCount

    SIZE_TO_DW(MS3DPRINT_OSP_SIZE),                     // dwSize
    0x07, 0x00, 0x00, 0x00,                             // dwPropertyDataType  (1=REG_SZ, 4=REG_DWORD, 7=REG_MULTI_SZ)

    0x20, 0x00,                                         // wPropertyNameLength
    'M', 0x0, 'S', 0x0, '3', 0x0, 'D', 0x0,             // bPropertyName
    'P', 0x0, 'r', 0x0, 'i', 0x0, 'n', 0x0,
    't', 0x0, 'C', 0x0, 'o', 0x0, 'n', 0x0,
    'f', 0x0, 'i', 0x0, 'g', 0x0, 0x0, 0x0,

    SIZE_TO_DW(MS3DPRINT_CONFIG_SIZE),                  // dwPropertyDataLength

    // Data
    0x42, 0x00, 0x61, 0x00, 0x73, 0x00, 0x65, 0x00, 0x3D, 0x00, 0x53, 0x00, 0x44, 0x00, 0x00, 0x00,  /* Base=SD  */  
    0x4A, 0x00, 0x6F, 0x00, 0x62, 0x00, 0x33, 0x00, 0x44, 0x00, 0x4F, 0x00, 0x75, 0x00, 0x74, 0x00,  /* Job3DOut */  
    0x70, 0x00, 0x75, 0x00, 0x74, 0x00, 0x41, 0x00, 0x72, 0x00, 0x65, 0x00, 0x61, 0x00, 0x57, 0x00,  /* putAreaW */  
    0x69, 0x00, 0x64, 0x00, 0x74, 0x00, 0x68, 0x00, 0x3D, 0x00, 0x32, 0x00, 0x35, 0x00, 0x30, 0x00,  /* idth=250 */  
    0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x00, 0x00, 0x4A, 0x00, 0x6F, 0x00, 0x62, 0x00, 0x33, 0x00,  /* 000 Job3 */  
    0x44, 0x00, 0x4F, 0x00, 0x75, 0x00, 0x74, 0x00, 0x70, 0x00, 0x75, 0x00, 0x74, 0x00, 0x41, 0x00,  /* DOutputA */  
    0x72, 0x00, 0x65, 0x00, 0x61, 0x00, 0x44, 0x00, 0x65, 0x00, 0x70, 0x00, 0x74, 0x00, 0x68, 0x00,  /* reaDepth */  
    0x3D, 0x00, 0x32, 0x00, 0x36, 0x00, 0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x00, 0x00,  /* =260000  */  
    0x4A, 0x00, 0x6F, 0x00, 0x62, 0x00, 0x33, 0x00, 0x44, 0x00, 0x4F, 0x00, 0x75, 0x00, 0x74, 0x00,  /* Job3DOut */  
    0x70, 0x00, 0x75, 0x00, 0x74, 0x00, 0x41, 0x00, 0x72, 0x00, 0x65, 0x00, 0x61, 0x00, 0x48, 0x00,  /* putAreaH */  
    0x65, 0x00, 0x69, 0x00, 0x67, 0x00, 0x68, 0x00, 0x74, 0x00, 0x3D, 0x00, 0x32, 0x00, 0x37, 0x00,  /* eight=27 */  
    0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x30, 0x00, 0x00, 0x00, 0x66, 0x00, 0x69, 0x00, 0x6C, 0x00,  /* 0000 fil */  
    0x61, 0x00, 0x6D, 0x00, 0x65, 0x00, 0x6E, 0x00, 0x74, 0x00, 0x64, 0x00, 0x69, 0x00, 0x61, 0x00,  /* amentdia */  
    0x6D, 0x00, 0x65, 0x00, 0x74, 0x00, 0x65, 0x00, 0x72, 0x00, 0x3D, 0x00, 0x32, 0x00, 0x38, 0x00,  /* meter=28 */  
    0x35, 0x00, 0x30, 0x00, 0x00, 0x00, 0x00, 0x00                                                   /* 50       */  
};
```

有关扩展属性 OS 功能描述符的信息位于 *操作系统 \_ Desc \_ Ext \_Prop.doc* 文件中。 有关详细信息，请参阅 [MICROSOFT OS 描述符](/previous-versions/gg463179(v=msdn.10)) 。

## <a name="verifying-the-print-capabilities"></a>验证打印功能

设备在闪存中刻录了固件后，Windows 10 会自动检测该设备，并且会将打印功能存储在注册表中。

![安装兼容3d 打印机 ](images/installing-compatible-3d-printer.png)

IHV 会将设备的 VID/PID 更改为其自身，这一点非常重要。 永远不要使用供应商 ID (VID) 或其他现有设备的产品 ID (PID) ，因为操作系统将不能正确检测设备，因为 VID 和 PID 优先于操作系统描述符。

如果设备已正确安装，则设备应在 " **设备和打印机**" 中列出。

![“设备和打印机”](images/devices-and-printers-3d.png)

在 **设备管理器**中，可以验证匹配的设备 id 和兼容 id。

![“设备管理器”](images/device-manager-3d.png)

![设备管理器详细信息选项卡-匹配设备 id](images/device-manager-details-3d.png)

![设备管理器详细信息选项卡兼容 id](images/device-manager-details2-3d.png)

可以通过访问 **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 枚举 \\ USB**上的注册表来获取 USB 驱动程序属性。

![在 usb 注册表中编辑多字符串值](images/usb-registry-3d.png)

可以通过访问 **HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Control \\ 打印 \\ 打印机**上的注册表来获取3d 打印驱动程序的属性。

![在注册表中查看3d 打印驱动程序属性](images/printers-registry-3d.png)

## <a name="additional-resources"></a>其他资源

有关详细信息，请参阅以下文档和资源：

[Windows 中的3D 打印](https://www.microsoft.com/3d-print/windows-3d-printing)

[ (MSI 下载) 的3D 打印 SDK ](https://go.microsoft.com/fwlink/p/?LinkId=394375)

[Microsoft OS 描述符](/previous-versions/gg463179(v=msdn.10))

[USB 2.0 规范](https://www.usb.org/documents)

还可以联系 Microsoft 3D 印刷团队，请求)  (的 [三维打印问题](https://go.microsoft.com/fwlink/p/?LinkId=534751) ask3dprint@microsoft.com 。